---
title: friend (C++)
ms.date: 11/19/2018
f1_keywords:
- friend_cpp
helpviewer_keywords:
- member access, from friend functions
- friend classes [C++]
- friend keyword [C++]
ms.assetid: 8fe9ee55-d56f-40cd-9075-d9fb1375aff4
ms.openlocfilehash: 769720877cc58de530791b268811d7d01adad3e6
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62154475"
---
# <a name="friend-c"></a>friend (C++)

在某些情況下，它會授與成員層級存取不是類別的成員函式或個別的類別中的所有成員更方便項目。 只有類別實作器才能宣告它的 friend 是誰。 函式或類別不能將它自己宣告為任何類別的 friend。 在類別定義中，使用**friend**關鍵字和非成員函式或其存取權授與您類別的 private 和 protected 成員的其他類別的名稱。 在範本定義中，類型參數可以宣告為 friend。

## <a name="syntax"></a>語法

```
class friend F
friend F;
```

## <a name="friend-declarations"></a>friend 宣告

如果您宣告先前未宣告的 friend 函式，會將該函式匯出至封入 nonclass 範圍。

Friend 宣告中宣告的函式會視為它們必須使用已宣告**extern**關鍵字。 如需詳細資訊，請參閱 < [extern](extern-cpp.md)。

雖然可以在全域範圍函式的原型之前將此類函式宣告為 friend，但不可在其完整類別宣告出現之前將成員函式宣告為 friend。 下列程式碼示範失敗的原因：

```cpp
class ForwardDeclared;   // Class name is known.
class HasFriends
{
    friend int ForwardDeclared::IsAFriend();   // C2039 error expected
};
```

上述範例在範圍中輸入類別名稱 `ForwardDeclared`，不過，完整宣告 (明確地說是宣告函式 `IsAFriend` 的部分) 是未知的。 因此， **friend**類別中的宣告`HasFriends`會產生錯誤。

從 C + + 11 開始，有兩種類別的 friend 宣告：

```cpp
friend class F;
friend F;
```

如果最內層的命名空間中找不到任何現有的類別，該名稱，則第一種形式導入了新的類別 F。 **C + + 11**:第二個表單不會引進新的類別;它可以使用已宣告的類別，並使用必須在宣告樣板類型參數或為 friend 的 typedef 時使用。

使用`class friend F`時參考的型別具有尚未宣告：

```cpp
namespace NS
{
    class M
    {
        class friend F;  // Introduces F but doesn't define it
    };
}
```

```cpp
namespace NS
{
    class M
    {
        friend F; // error C2433: 'NS::F': 'friend' not permitted on data declarations
    };
}
```

在下列範例中，`friend F`是指`F`NS 的範圍外宣告的類別。

```cpp
class F {};
namespace NS
{
    class M
    {
        friend F;  // OK
    };
}
```

使用`friend F`宣告為 friend 樣板參數：

```cpp
template <typename T>
class my_class
{
    friend T;
    //...
};
```

使用`friend F`宣告為 friend 的 typedef:

```cpp
class Foo {};
typedef Foo F;

class G
{
    friend F; // OK
    friend class F // Error C2371 -- redefinition
};
```

若要宣告兩個類別為彼此的 Friend，必須將第二個類別完整指定為第一個類別的 friend。 這項限制的理由是編譯器的資訊只足以在宣告第二個類別的點宣告個別 friend 函式。

> [!NOTE]
>  雖然整個第二個類別必須是第一個類別的 friend，但您可以第一個類別中的哪些函式是第二個類別的 friend。

## <a name="friend-functions"></a>friend 函式

A **friend**函式是不是類別的成員，但可以存取類別的 private 和 protected 成員的函式。 friend 函式並非類別成員，而是擁有特殊存取權限的一般外部函式。 Friend 不在類別的範圍就它們不會呼叫使用成員選取運算子 (**。** 和-**>**) 除非它們是另一個類別的成員。 A **friend**授與存取權的類別所宣告函式。 **Friend**宣告可放在任何類別宣告中。 不會受存取控制關鍵字的影響。

下列範例顯示 `Point` 類別和 friend 函式 `ChangePrivate`。 **Friend**函式有權存取的私用資料成員`Point`物件收到做為參數。

```cpp
// friend_functions.cpp
// compile with: /EHsc
#include <iostream>

using namespace std;
class Point
{
    friend void ChangePrivate( Point & );
public:
    Point( void ) : m_i(0) {}
    void PrintPrivate( void ){cout << m_i << endl; }

private:
    int m_i;
};

void ChangePrivate ( Point &i ) { i.m_i++; }

int main()
{
   Point sPoint;
   sPoint.PrintPrivate();
   ChangePrivate(sPoint);
   sPoint.PrintPrivate();
// Output: 0
           1
}
```

## <a name="class-members-as-friends"></a>做為 friend 的類別成員

類別成員函式可以宣告為其他類別的 friend。 參考下列範例：

```cpp
// classes_as_friends1.cpp
// compile with: /c
class B;

class A {
public:
   int Func1( B& b );

private:
   int Func2( B& b );
};

class B {
private:
   int _b;

   // A::Func1 is a friend function to class B
   // so A::Func1 has access to all members of B
   friend int A::Func1( B& );
};

int A::Func1( B& b ) { return b._b; }   // OK
int A::Func2( B& b ) { return b._b; }   // C2248
```

上述範例只授與 `A::Func1( B& )` 函式類別 `B` 的 friend 存取權限。 因此，存取私用成員`_b`一體`Func1`類別的`A`但無法在`Func2`。

`friend` 類別是其所有成員函式皆為某個類別之 friend 函式的類別，也就是說，其成員函式可以存取其他類別的 private 成員和 protected 成員。 假設 `friend` 類別中的 `B` 宣告如下：

```cpp
friend class A;
```

在這種情況下，`A` 類別中的所有成員函式將獲得類別 `B` 的 friend 存取權限。 下列程式碼是 friend 類別的範例：

```cpp
// classes_as_friends2.cpp
// compile with: /EHsc
#include <iostream>

using namespace std;
class YourClass {
friend class YourOtherClass;  // Declare a friend class
public:
   YourClass() : topSecret(0){}
   void printMember() { cout << topSecret << endl; }
private:
   int topSecret;
};

class YourOtherClass {
public:
   void change( YourClass& yc, int x ){yc.topSecret = x;}
};

int main() {
   YourClass yc1;
   YourOtherClass yoc1;
   yc1.printMember();
   yoc1.change( yc1, 5 );
   yc1.printMember();
}
```

除非明確指定，否則夥伴關係不是雙向的。 在上述範例中，`YourClass` 的成員函式無法存取 `YourOtherClass` 的 private 成員。

Managed 型別不能包含任何 friend 函式、friend 類別或 friend 介面。

夥伴關係不能繼承，也就是說，衍生自 `YourOtherClass` 的類別不能存取 `YourClass` 的 private 成員。 夥伴關係不可轉移，因此，若類別屬於 `YourOtherClass` 的 friend，就無法存取 `YourClass` 的 private 成員。

下圖說明四種類別宣告：`Base`、`Derived`、`aFriend` 和 `anotherFriend`。 只有類別 `aFriend` 可以直接存取 `Base` 的 private 成員 (以及 `Base` 可能繼承的任何成員)。

![Friend 關聯性的含意](../cpp/media/vc38v41.gif "friend 關聯性的含意") <br/>
friend 關聯性的含意

## <a name="inline-friend-definitions"></a>內嵌 friend 定義

Friend 函式可以在類別宣告內定義。 這些函式為內嵌函式，而且如同成員內嵌函式一般，它們就像是緊接著在已查看所有類別成員之後，類別範圍關閉之前 (類別宣告的結尾) 所定義。

在類別宣告內定義的 friend 函式不會視為在封入類別的範圍內，而是在檔案範圍內。

## <a name="see-also"></a>另請參閱

[關鍵字](../cpp/keywords-cpp.md)