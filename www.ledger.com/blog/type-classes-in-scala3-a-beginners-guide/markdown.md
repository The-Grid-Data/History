[ New: Wallet recovery made easy with Ledger Recover, provided by Coincover
Get started ](https://shop.ledger.com/pages/ledger-recover)

Our Website now exists in . Do you want to change languages?

Yes, please No, I'm good

You can revert to English at any time by clicking on the language menu on the
top right corner of the page.

[ ![Ledger](https://www.ledger.com/wp-
content/themes/ledger-v2/public/images/ledger-logo-long.svg)
](https://www.ledger.com "Ledger")

  * Products
    * [Ledger Stax](https://shop.ledger.com/pages/ledger-stax "Ledger Stax")
    * [Ledger Nano X](https://shop.ledger.com/pages/ledger-nano-x "Ledger Nano X")
    * [Ledger Nano S Plus](https://shop.ledger.com/pages/ledger-nano-s-plus "Ledger Nano S Plus")
    * [Compare our devices](https://shop.ledger.com/pages/hardware-wallets-comparison "Compare our devices")
    * [Packs](https://shop.ledger.com/#category-bundle "Packs")
    * [Accessories](https://shop.ledger.com/#category-accessories "Accessories")
    * [Collaborations](https://www.ledger.com/collaborations "Collaborations")
    * [See all products](https://shop.ledger.com "See all products")
    * [Download Ledger Live](https://www.ledger.com/ledger-live "Download Ledger Live")
    * [Supported crypto](https://www.ledger.com/supported-crypto-assets "Supported crypto")
  * App and services
    * [Ledger Live](https://www.ledger.com/ledger-live "Ledger Live")
    * [Ledger Recover](https://shop.ledger.com/pages/ledger-recover "Ledger Recover")
    * [CL Card](https://www.ledger.com/cl-card "CL Card")
    * [Supported Services](https://www.ledger.com/supported-services "Supported Services")
    * [Crypto Prices](https://www.ledger.com/coin/price "Crypto Prices")
  * Learn
    * [Ledger Academy](https://www.ledger.com/academy "Ledger Academy")
    * [Learn and Earn](https://quest.ledger.com/ "Learn and Earn")
    * [Classroom](https://www.ledger.com/academy/what-is-web-30-everything-you-need-to-know "Classroom")
    * [Blog](/blog "Blog")
    * [What is a crypto wallet](https://www.ledger.com/academy/basic-basics/2-how-to-own-crypto/what-is-a-crypto-wallet "What is a crypto wallet")
    * [How to Buy](https://www.ledger.com/buy "How to Buy")
    * [How to Swap](https://www.ledger.com/swap "How to Swap")
    * [How to Stake](https://www.ledger.com/staking "How to Stake")
  * For Business
    * [Ledger Enterprise Solutions](https://enterprise.ledger.com?utm_source=mainsite&utm_medium=header "Ledger Enterprise Solutions")
    * [Ledger Partners](/partners "Ledger Partners")
    * [Ledger Co-branded Partnership](https://co-branded.ledger.com/ "Ledger Co-branded Partnership")
  * [For Developers](https://developers.ledger.com/ "For Developers")
  * [Support](https://support.ledger.com/hc "Support")
  * English
    * This page is available in English only

[__](https://shop.ledger.com/cart "Ledger Shop")

__

[Blog](https://www.ledger.com/blog/type-classes-in-scala3-a-beginners-guide)
__[Blog posts](https://www.ledger.com/category/blog-posts "Blog posts")

[Blog posts](https://www.ledger.com/category/blog-posts "Blog posts"), [Tech](https://www.ledger.com/category/tech "Tech") | 12/19/2023 

# Type Classes in Scala3: A Beginner’s Guide

[Blog](https://www.ledger.com/blog/type-classes-in-scala3-a-beginners-guide)
__[Blog posts](https://www.ledger.com/category/blog-posts "Blog posts")

This document is intended for the beginner Scala3 developer who is already
versed in Scala prose, but is puzzled about all the ``implicits`` and
parameterized traits in the code.

This document explains the why, how, where and when of **Type Classes (TC)**.

After reading this document the beginner Scala3 developer will gain solid
knowledge to use and dive into the source code of _a lot_ of Scala libraries
and start writing idiomatic Scala code.

Let’s start with the why…

###### Table of Content

  * The expression problem
    * Rule 1: implementation of existing behavior on new representation
    * Rule 2: implementation of new behaviors to be applied to existing representations
  * The Type Class pattern
    * 1\. Define a new behavior
    * 2\. Implement the behavior
    * 3\. Use the behavior
    * Discussion
  * Enhanced developer experience
    * Implicits
    * Implicits sugars
    * Extension
    * Generic type with TC
    * Automatic derivation
  * Summary of all the benefits
  * Counter indications
  * Conclusion

#### The expression problem

In 1998, [Philip Wadler
stated](https://homepages.inf.ed.ac.uk/wadler/papers/expression/expression.txt)
that “the expression problem is a new name for an old problem”. It’s the
problem of software extensibility. According to mister Wadler writing, the
solution to the expression problem must comply to the following rules:

  * Rule 1: Allow the implementation of **existing behaviors** (think of Scala trait) to be applied to **new representations** (think of a case class )
  * Rule 2:  Allow the implementation of **new behaviors** to be applied to **existing representations**
  * Rule 3: It must not jeopardize the**type safety**
  * Rule 4: It must not necessitate to recompile **existing code**

Solving this problem will be the silver thread of this article.

##### Rule 1: implementation of existing behavior on new representation

Any object oriented language has a baked-in solution for rule 1 with **subtype
polymorphism**. You can safely implement any ``trait`` defined in a dependency
on a ``class`` in your own code, without recompiling the dependency. Let’s see
that in action:

Scala

    
    
    def todo = 42
    type Height = Int
    type Block = Int
    
    object Lib1:
      trait Blockchain:
        def getBlock(height: Height): Block
    
      case class Ethereum() extends Blockchain:
        override def getBlock(height: Height) = todo
    
      case class Bitcoin() extends Blockchain:
        override def getBlock(height: Height) = todo
    
    
    object Lib2:
      import Lib1.*
    
      case class Polkadot() extends Blockchain:
        override def getBlock(height: Height): Block = todo
    
    val eth = Lib1.Ethereum()
    val btc = Lib1.Bitcoin()
    val dot = Lib2.Polkadot()

[Source](https://github.com/jprudent/type-class-
article/blob/6b8b5932c867971fa5f88d44a798a42e77adfce5/main.sc)

In this fictitious example, library ``Lib1`` (line 5) defines a trait
``Blockchain`` (line 6) with 2 implementations of it (lines 9 & 12).**``Lib1``
will remain the same in ALL this document (enforcement of rule 4).**  
  
``Lib2`` (line 15) implements the existing behavior ``Blockchain`` on a new
class ``Polkadot`` (rule 1) in a type safe (rule 3) manner, without
recompiling ``Lib1`` (rule 4).

##### Rule 2: implementation of new behaviors to be applied to existing
representations

Let’s imagine in ``Lib2`` we want a new behavior ``lastBlock`` to be
implemented specifically for each ``Blockchain``.

First thing that comes to mind is creating a big switch based on the type of
parameter.

Scala

    
    
    def todo = 42
    type Height = Int
    type Block = Int
    
    object Lib1:
      trait Blockchain:
        def getBlock(height: Height): Block
    
      case class Ethereum() extends Blockchain:
        override def getBlock(height: Height) = todo
    
      case class Bitcoin() extends Blockchain:
        override def getBlock(height: Height) = todo
    
    object Lib2:
      import Lib1.*
    
      case class Polkadot() extends Blockchain:
        override def getBlock(height: Height): Block = todo
    
      def lastBlock(blockchain: Blockchain): Block = blockchain match
          case _:Ethereum => todo
          case _:Bitcoin  => todo
          case _:Polkadot => todo
      
    
    object Lib3:
      import Lib1.*
    
      case class Polygon() extends Blockchain:
        override def getBlock(height: Height): Block = todo
    
    import Lib1.*, Lib2.*, Lib3.*
    println(lastBlock(Bitcoin()))
    println(lastBlock(Ethereum()))
    println(lastBlock(Polkadot()))
    println(lastBlock(Polygon()))

[Source](https://github.com/jprudent/type-class-
article/blob/bb3f3109c5d23c9b8508639f339f4065032fe673/main.sc)

This solution is a weak reimplementation of type based polymorphism that is
already baked-in language!

``Lib1`` is left untouched (remember, enforced rule 4 all over this document).

The solution implemented in ``Lib2`` is _okayish_ until yet another blockchain
is introduced in ``Lib3``. It infringes the type safety rule (rule 3) because
this code fails at runtime on line 37. And modifying ``Lib2`` would infringe
rule 4.

Another solution is using an ``extension``.

Scala

    
    
    def todo = 42
    type Height = Int
    type Block = Int
    
    object Lib1:
      trait Blockchain:
        def getBlock(height: Height): Block
    
      case class Ethereum() extends Blockchain:
        override def getBlock(height: Height) = todo
    
      case class Bitcoin() extends Blockchain:
        override def getBlock(height: Height) = todo
    
    object Lib2:
      import Lib1.*
    
      case class Polkadot() extends Blockchain:
        override def getBlock(height: Height): Block = todo
    
        def lastBlock(): Block = todo
    
      extension (eth: Ethereum) def lastBlock(): Block = todo
    
      extension (btc: Bitcoin) def lastBlock(): Block = todo
    
    import Lib1.*, Lib2.*
    println(Bitcoin().lastBlock())
    println(Ethereum().lastBlock())
    println(Polkadot().lastBlock())
    
    def polymorphic(blockchain: Blockchain) =
      // blockchain.lastBlock()
      ???

[Source](https://github.com/jprudent/type-class-
article/blob/64b978f238f9dc09d88dfd51ac1084d606e03053/main.sc)

``Lib1`` is left untouched (enforcement of rule 4 in the whole document).

``Lib2`` defines behavior for its type (line 21) and `extension`s for existing
types (lines 23 & 25).

Lines 28-30, the new behavior can be used in each class.

But there is no way to call this new behavior polymorphically (line 32). Any
attempt to do so leads to compilation errors (line 33) or to type based
switches.

This Rule n°2 is tricky. We tried to implement it with our own definition of
polymorphism and `extension` trick. And that was weird.

There is a missing piece called _ad-hoc polymorphism:_ the ability to safely
dispatch a behavior implementation according to a type, wherever the behavior
and type are defined. Enter the _Type Class_ pattern.

#### The Type Class pattern

The Type Class (TC for short) pattern recipe has 3 steps.

  1. Define a new behavior
  2. Implement the behavior
  3. Use the behavior

In the following section, I implement the TC pattern in the most
straightforward way. It’s verbose, clunky and impractical. But hold on, those
caveats will be fixed step by step further in the document.

##### 1\. Define a new behavior

Scala

    
    
    object Lib2:
      import Lib1.*
    
      trait LastBlock[A]:
        def lastBlock(instance: A): Block

[Source](https://github.com/jprudent/type-class-
article/blob/323ae6432a327fcff4f62f214b70cc57af4ad1d0/main.sc)

``Lib1`` is, once again, left untouched.

The new behavior **is** the TC materialized by the trait. The functions
defined in the trait are a way to apply some aspects of that behavior.

The parameter ``A`` represents the type we want to apply behavior to, which
are subtypes of ``Blockchain`` in our case.

Some remarks:

  * If needed, the parameterized type ``A`` can be further constrained by the Scala type system. For instance, we could enforce ``A`` to be a ``Blockchain``. 
  * Also, the TC could have many more functions declared in it.
  * Finally, each function may have many more arbitrary parameters.

But let’s keep things simple for the sake of readability.

##### 2\. Implement the behavior

Scala

    
    
    object Lib2:
      import Lib1.*
    
      trait LastBlock[A]:
        def lastBlock(instance: A): Block
    
      val ethereumLastBlock = new LastBlock[Ethereum]:
        def lastBlock(eth: Ethereum) = eth.lastBlock
    
      val bitcoinLastBlock = new LastBlock[Bitcoin]:
        def lastBlock(btc: Bitcoin) = http("http://bitcoin/last")

[Source](https://github.com/jprudent/type-class-
article/blob/323ae6432a327fcff4f62f214b70cc57af4ad1d0/main.sc)

For each type the new ``LastBlock`` behavior is expected, there is a specific
instance of that behavior.

The ``Ethereum`` implementation line 22 is computed from the ``eth`` instance
passed as parameter.

The implementation of ``LastBlock`` for ``Bitcoin`` line 25 is implemented
with an unmanaged IO and doesn’t use its parameter.

So, ``Lib2`` implements new behavior ``LastBlock`` for ``Lib1`` classes.

##### 3\. Use the behavior

Scala

    
    
    object Lib2:
      import Lib1.*
    
      trait LastBlock[A]:
        def lastBlock(instance: A): Block
    
      val ethereumLastBlock = new LastBlock[Ethereum]:
        def lastBlock(eth: Ethereum) = eth.lastBlock
    
      val bitcoinLastBlock = new LastBlock[Bitcoin]:
        def lastBlock(btc: Bitcoin) = http("http://bitcoin/last")
    
    import Lib1.*, Lib2.*
    
    def useLastBlock[A](instance: A, behavior: LastBlock[A]) =
      behavior.lastBlock(instance)
    
    println(useLastBlock(Ethereum(lastBlock = 2), ethereumLastBlock))
    println(useLastBlock(Bitcoin(), bitcoinLastBlock))

[Source](https://github.com/jprudent/type-class-
article/blob/323ae6432a327fcff4f62f214b70cc57af4ad1d0/main.sc)

Line 30 ``useLastBlock`` uses an instance of ``A`` and the ``LastBlock``
behavior defined for that instance.

Line 33 ``useLastBlock`` is called with an instance of ``Ethereum`` and an
implementation of ``LastBlock`` defined in ``Lib2``. Note that it’s possible
to pass any alternative implementation of ``LastBlock[A]`` (think of
_dependency injection_).

``useLastBlock`` is the glue between representation (the actual A) and its
behavior. Data and behavior are separated, which is what functional
programming advocates for.

##### Discussion

Let’s recap the rules of the expression problem:

  * Rule 1: Allow the implementation of **existing behaviors**   to be applied to **new classes**
  * Rule 2:  Allow the implementation of **new behaviors** to be applied to **existing classes**
  * Rule 3: It must not jeopardize the**type safety**
  * Rule 4: It must not necessitate to recompile **existing code**

Rule 1 can be solved out of the box with subtype polymorphism.

The TC pattern just presented (see previous screenshot) solves rule 2. It’s
type safe (rule 3) and we never touched ``Lib1`` (rule 4).

However it’s impractical to use for several reason:

  * Lines 33-34 we have to explicitly pass the behavior along its instance. This is an extra overhead. We should just write ``useLastBlock(Bitcoin())``.
  * Line 31 the syntax is uncommon.  We would rather prefer to write a concise and more object oriented  ``instance.lastBlock()`` statement.

Let’s highlight some Scala features for practical TC usage.

#### Enhanced developer experience

Scala has a unique set of features and syntactic sugars that makes TC a truly
enjoyable experience for developers.

##### Implicits

The implicit scope is a special scope resolved at compile time where only one
instance of a given type can exist.

A program puts an instance in the implicit scope with the ``given`` keyword.
Alternatively a program can retrieve an instance from the implicit scope with
keyword ``using``.

The implicit scope is resolved at compile time, there is no way to change it
dynamically at runtime. If the program compiles, the implicit scope is
resolved. At runtime, it’s not possible to have missing implicit instances
where they are used. The only possible confusion may come from using the wrong
implicit instance, but this issue is left for the creature between the chair
and the keyboard.

It’s different from a global scope because:

  1. It’s resolved contextually. Two locations of a program can use an instance of the same given type in implicit scope, but those two instances may be different.
  2. Behind the scene the code is passing implicit arguments function to function until the implicit usage is reached. It’s not using a global memory space.

Going back to the type class! Let’s take the exact same example.

Scala

    
    
    def todo = 42
    type Height = Int
    type Block = Int
    def http(uri: String): Block = todo
    
    object Lib1:
      trait Blockchain:
        def getBlock(height: Height): Block
    
      case class Ethereum() extends Blockchain:
        override def getBlock(height: Height) = todo
    
      case class Bitcoin() extends Blockchain:
        override def getBlock(height: Height) = todo

``Lib1`` is the same unmodified code we previously defined.

Scala

    
    
    object Lib2:
      import Lib1.*
    
      trait LastBlock[A]:
        def lastBlock(instance: A): Block
    
      given ethereumLastBlock:LastBlock[Ethereum] = new LastBlock[Ethereum]:
        def lastBlock(eth: Ethereum) = eth.lastBlock
    
      given bitcoinLastBlock:LastBlock[Bitcoin] = new LastBlock[Bitcoin]:
        def lastBlock(btc: Bitcoin) = http("http://bitcoin/last")
    
    import Lib1.*, Lib2.*
    
    def useLastBlock[A](instance: A)(using behavior: LastBlock[A]) =
      behavior.lastBlock(instance)
    
    println(useLastBlock(Ethereum(lastBlock = 2)))
    println(useLastBlock(Bitcoin()))

[Source](https://github.com/jprudent/type-class-
article/blob/173e87f836d7ac0cbcb2e7265ae07217f2c424ab/main.sc)

Line 19 a new behavior ``LastBlock`` is defined, exactly like we did
previously.

Line 22 and line 25, ``val`` is replaced by ``given``. Both implementations of
``LastBlock`` are put in the implicit scope.

Line 31 ``useLastBlock`` declares the behavior ``LastBlock`` as an implicit
parameter. The compiler resolves the appropriate instance of ``LastBlock``
from implicit scope contextualized from caller locations (lines 33 and 34).
Line 28 imports everything from ``Lib2``, including the implicit scope. So,
the compiler passes instances defined lines 22 and 25 as the last parameter of
``useLastBlock``.

As a library user, using a type class is easier than before. Line 34 and 35 a
developer has only to make sure that an instance of the behavior is injected
in the implicit scope (and this can be a mere ``import``). If an implicit is
not ``given`` where the code is ``using`` it, the compiler tells him.

Scala’s implicit ease the task of passing class instances along with instances
of their behaviors.

##### Implicit sugars

Line 22 and 25 of previous code can be further improved ! Let’s iterate on the
TC implementations.

Scala

    
    
    given LastBlock[Ethereum] = new LastBlock[Ethereum]:
        def lastBlock(eth: Ethereum) = eth.lastBlock
    
      given LastBlock[Bitcoin] = new LastBlock[Bitcoin]:
        def lastBlock(btc: Bitcoin) = http("http://bitcoin/last")
    

[Source](https://github.com/jprudent/type-class-
article/blob/396cd07bf1d0c0ff3aa142cf9756c098e6f3ddb3/main.sc)

Lines 22 and 25, if the name of the instance is unused, it can be omitted.

Scala

    
    
      given LastBlock[Ethereum] with
        def lastBlock(eth: Ethereum) = eth.lastBlock
    
      given LastBlock[Bitcoin] with
        def lastBlock(btc: Bitcoin) = http("http://bitcoin/last")

[Source](https://github.com/jprudent/type-class-
article/blob/47ce38569321738c5efe60ef37480b3cd768ae61/main.sc)

Lines 22 and 25, the repetition of the type can be replaced with ``with``
keyword.

Scala

    
    
    given LastBlock[Ethereum] = _.lastBlock
    
      given LastBlock[Bitcoin] = _ => http("http://bitcoin/last")

[Source](https://github.com/jprudent/type-class-
article/blob/48888cfeb2638dde245e5de847e2363b340f0c4c/main.sc)

Because we use a degenerated trait with a single function in it, the IDE may
suggest simplifying the code with a SAM expression. Although correct, I don’t
think it’s a proper use of SAM, unless you’re casually code golfing.

Scala offers syntactic sugars to streamline the syntax, removing unnecessary
naming, declaration and type redundancy.

##### Extension

Used wisely, the ``extension`` mechanism can simplify the syntax for using a
type class.

Scala

    
    
    object Lib2:
      import Lib1.*
    
      trait LastBlock[A]:
        def lastBlock(instance: A): Block
    
      given LastBlock[Ethereum] with
        def lastBlock(eth: Ethereum) = eth.lastBlock
    
      given LastBlock[Bitcoin] with
        def lastBlock(btc: Bitcoin) = http("http://bitcoin/last")
    
      extension[A](instance: A)
        def lastBlock(using tc: LastBlock[A]) = tc.lastBlock(instance)
    
    import Lib1.*, Lib2.*
    
    println(Ethereum(lastBlock = 2).lastBlock)
    println(Bitcoin().lastBlock)

[Source](https://github.com/jprudent/type-class-
article/blob/e254ec80c7e63a72c6842cfc8aa710b49f8c7862/main.sc)

Lines 28-29 a generic extension method ``lastBlock`` is defined for any ``A``
with a ``LastBlock`` TC parameter in implicit scope.

Lines 33-34 the extension leverages an object oriented syntax to use TC.

Scala

    
    
    object Lib2:
      import Lib1.*
    
      trait LastBlock[A]:
        def lastBlock(instance: A): Block
    
      given LastBlock[Ethereum] with
        def lastBlock(eth: Ethereum) = eth.lastBlock
    
      given LastBlock[Bitcoin] with
        def lastBlock(btc: Bitcoin) = http("http://bitcoin/last")
    
      extension[A](instance: A)(using tc: LastBlock[A])
        def lastBlock = tc.lastBlock(instance)
        def penultimateBlock = tc.lastBlock(instance) - 1
    
    import Lib1.*, Lib2.*
    
    val eth = Ethereum(lastBlock = 2)
    println(eth.lastBlock)
    println(eth.penultimateBlock)
    
    val btc = Bitcoin()
    println(btc.lastBlock)
    println(btc.penultimateBlock)

[Source](https://github.com/jprudent/type-class-
article/blob/91028348933afc645287cff05cfa7a6ed7a747ab/main.sc)

Line 28, the TC parameter can also be defined for the whole extension to avoid
repetition. Line 30 we reuse the TC in the extension to define
``penultimateBlock`` (even though it could be implemented on ``LastBlock``
trait directly)

The magic happens when the TC is used. The expression feels a lot more
natural, giving the illusion that behavior ``lastBlock`` is conflated with the
instance.

##### Generic type with TC

Scala

    
    
    import Lib1.*, Lib2.*
    
    def useLastBlock1[A](instance: A)(using LastBlock[A]) = instance.lastBlock
    
    def useLastBlock2[A: LastBlock](instance: A) = instance.lastBlock
    
    val eth = Ethereum(lastBlock = 2)
    assert(useLastBlock1(eth) == useLastBlock2(eth))

[Source](https://github.com/jprudent/type-class-
article/blob/d73b62b892a42cdee1ae378ea8b3a85de90e0be5/main.sc)

Line 34 the function uses an implicit TC. Note that the TC doesn’t need to be
named if that name is unnecessary.

The TC pattern is so widely used that there is a generic type syntax to
express “a type with an implicit behavior”. Line 36 the syntax is a more
concise alternative to the previous one (line 34). It avoids declaring
specifically the unnamed implicit TC parameter.

This concludes the developer experience section. We have seen how extensions,
implicits and some syntactic sugar can provide a less cluttered syntax when
the TC is used and defined.

##### Automatic derivation

A lot of Scala libraries use TC, leaving the programmer to implement them in
their code base.

For instance Circe (a json de-serialization library) uses TC ``Encoder[T]``
and ``Decoder[T]`` for programmers to implement in their codebase. Once
implemented the whole scope of the library can be used.

Those implementations of TC are more than often **data oriented mappers**.
They don’t need any business logic, are boring to write, and a burden to
maintain in sync with case classes.

In such a situation, those libraries offer what is called **automatic**
derivation or **semi-automatic** derivation. See for instance Circe[
automatic](https://web.archive.org/web/20221027022726/https://circe.github.io/circe/codecs/auto-
derivation.html) and[ semi-
automatic](https://web.archive.org/web/20221127094623/https://circe.github.io/circe/codecs/semiauto-
derivation.html) derivation. With semi-automatic derivation the programmer can
declare an instance of a type class with some minor syntax, whereas automatic
derivation doesn’t necessitate any code modification except for an import.

Under the hood, at compile time, generic macros introspect _types_ as pure
data structure and generate a TC[T] for library users.

Deriving generically a TC is very common, so Scala introduced a complete tool
box for that purpose. This method is not always advertised by library
documentations although it’s the Scala 3 way of using derivation.

Scala

    
    
    object GenericLib:
    
      trait Named[A]:
        def blockchainName(instance: A): String
    
      object Named:
        import scala.deriving.*
    
        inline final def derived[A](using inline m: Mirror.Of[A]): Named[A] =
          val nameOfType: String = inline m match
            case p: Mirror.ProductOf[A] => compiletime.constValue[p.MirroredLabel]
            case _ => compiletime.error("Not a product")
          new Named[A]:
            override def blockchainName(instance: A):String = nameOfType.toLowerCase
    
      extension[A] (instance: A)(using tc: Named[A])
        def blockchainName = tc.blockchainName(instance)
    
    import Lib1.*, GenericLib.*
    
    case class Polkadot() derives Named
    given Named[Bitcoin] = Named.derived
    given Named[Ethereum] = Named.derived
    
    println(Ethereum(lastBlock = 2).blockchainName)
    println(Bitcoin().blockchainName)
    println(Polkadot().blockchainName)

[Source](https://github.com/jprudent/type-class-
article/blob/31c6c713513aef8fd73b62c1983e8a21692d2c28/main.sc)

Line 18 a new TC ``Named`` is introduced. This TC is unrelated to the
blockchain business strictly speaking. Its purpose is to name the blockchain
based on the name of the case class.  

First focus on definitions lines 36-38. There are 2 syntaxes for deriving a
TC:

  1. Line 36 the TC instance can be defined directly on the case class with the ``derives`` keyword. Under the hood the compiler generates a given ``Named`` instance in ``Polkadot`` companion object.
  2. Line 37 and 38, type classes instances are given on pre-existing classes with ``TC.derived`` 

Line 31 a generic extension is defined (see previous sections) and
``blockchainName`` is used naturally.  

The ``derives`` keyword expects a method with the form ``inline def
derived[T](using Mirror.Of[T]): TC[T] = ???`` which is defined line 24. I
won’t explain in depth what the code does. In broad outlines:

  * ``inline def`` defines a macro
  * ``Mirror`` is part of the toolbox to introspect types. There are different kinds of mirrors, and line 26 the code focuses on ``Product`` mirrors (a case class is a product). Line 27, if programmers try to derive something that is not a ``Product``, the code won’t compile.
  * the ``Mirror`` contains other types. One of them, ``MirrorLabel``, is a string that contains the type name. This value is used in the implementation, line 29, of the ``Named`` TC.

TC authors can use meta programming to provide functions that generically
generate instances of TC given a type. Programmers can use dedicated library
API or the Scala deriving tools to create instances for their code.

Whether you need generic or specific code to implement a TC, there is a
solution for each situation.

#### Summary of all the benefits

  * It solves the expression problem 
    * New types can implement existing behavior through traditional trait inheritance
    * New behaviors can be implemented on existing types
  * Separation of concern 
    * The code is not mangled and easily deletable. A TC separates data and behavior, which is a functional programming motto.
  * It’s safe 
    * It’s type safe because it doesn’t rely on introspection. It avoids big pattern matching involving types. if you encounter yourself writing such code, you may detect a case where TC pattern will suit perfectly.
    * The implicit mechanism is compile safe! If an instance is missing at compile time the code won’t compile. No surprise at runtime.
  * It brings ad-hoc polymorphism 
    * Ad hoc polymorphism is usually missing in traditional object oriented programming.
    * With ad-hoc polymorphism, developers can implement the same behavior for various unrelated types without using traditional sub typing (which couples the code)
  * Dependency injection made easy 
    * A TC instance can be changed in respect of Liskov substitution principle. 
    * When a component has a dependency upon a TC, a mocked TC can easily be injected for testing purposes. 

#### Counter indications

Every hammer is designed for a range of problems.

Type Classes are for behavioral problems and must not be used for data
inheritance. Use composition for that purpose.

The usual subtyping is more straightforward. If you own the code base and
don’t aim for extensibility, type classes may be overkill.

For instance, In Scala core, there is a ``Numeric`` type class:

Scala

    
    
    trait Numeric[T] extends Ordering[T] {
      def plus(x: T, y: T): T
      def minus(x: T, y: T): T
      def times(x: T, y: T): T

[Source](https://github.com/scala/scala/blob/2.13.x/src/library/scala/math/Numeric.scala#L221)

It really makes sense to use such a type class because it not only allows
reuse of algebraic algorithms on types that are embedded in Scala (Int,
BigInt, …), but also on user defined types (a ``ComplexNumber`` for instance).

On the other hand, implementation of Scala collections mostly use subtyping
instead of type class. This design makes sense for several reason:

  * The collection API is supposed to be complete and stable. It exposes common behavior through traits inherited by implementations. Being highly extensible is not a particular goal here.
  * It must be simple to use. TC adds a mental overhead on the end user programmer.
  * TC might also incur small overhead in performance. This may be critical for a collection API.
  * Though, the collection API is still extensible through new TC defined in by third party libraries.

#### Conclusion

We’ve seen that TC is a simple pattern that solves a big problem. Thanks to
Scala rich syntax, the TC pattern can be implemented and used in many ways.
The TC pattern is in line with the functional programming paradigm and is a
fabulous tool for a clean architecture. There is no silver bullet and TC
pattern must be applied when it fits.

Hope you gained knowledge reading this document.

Code is available at <https://github.com/jprudent/type-class-article>. Please
reach out to me if you have any sort of questions or remarks. You can use
issues or code comments in the repository if you want.

* * *

[Jerome PRUDENT](https://www.linkedin.com/in/jprudent)

Software Engineer

[](https://www.facebook.com/Ledger/)
[__](https://www.instagram.com/ledger/)[](https://twitter.com/Ledger)
[](https://www.linkedin.com/company/ledgerhq/)
[](https://www.reddit.com/r/ledgerwallet/)
[__](https://www.tiktok.com/@ledger)

More articles

[](https://www.ledger.com/blog-ledger-stax-now-shipping-a-message-from-
ledgers-ceo-pascal-gauthier "Ledger Stax Now Shipping: A Message From Ledger’s
CEO Pascal Gauthier")

[Blog posts](https://www.ledger.com/category/blog-posts "Blog posts"), [Company](https://www.ledger.com/category/company-news "Company") | 05/28/2024 

Ledger Stax Now Shipping: A Message From Ledger’s CEO Pascal Gaut...

[Read more](https://www.ledger.com/blog-ledger-stax-now-shipping-a-message-
from-ledgers-ceo-pascal-gauthier "Ledger Stax Now Shipping: A Message From
Ledger’s CEO Pascal Gauthier")

[](https://www.ledger.com/blog-cargo-checkct-our-home-made-tool-guarding-
against-timing-attacks-is-now-open-source "Cargo-checkct: our home-made tool
guarding against timing attacks is now open-source!")

[Blog posts](https://www.ledger.com/category/blog-posts "Blog posts"), [Donjon](https://www.ledger.com/category/donjon "Donjon") | 05/17/2024 

Cargo-checkct: our home-made tool guarding against timing attacks...

[Read more](https://www.ledger.com/blog-cargo-checkct-our-home-made-tool-
guarding-against-timing-attacks-is-now-open-source "Cargo-checkct: our home-
made tool guarding against timing attacks is now open-source!")

[](https://www.ledger.com/blog/device-apps-tutorials "Master Ledger Device
Apps development with step-by-step tutorials")

[Blog posts](https://www.ledger.com/category/blog-posts "Blog posts"), [Tech](https://www.ledger.com/category/tech "Tech") | 05/07/2024 

Master Ledger Device Apps development with step-by-step tutorials...

[Read more](https://www.ledger.com/blog/device-apps-tutorials "Master Ledger
Device Apps development with step-by-step tutorials")

### Stay in touch

Announcements can be found in our blog. Press contact:  
[media@ledger.com](mailto:media@ledger.com)

  * [__](https://www.reddit.com/r/ledgerwallet/ "Ledger Reddit")
  * [__](https://www.facebook.com/Ledger/ "Ledger Facebook")
  * [__](https://www.instagram.com/ledger/ "Ledger Instagram")
  * [__](https://twitter.com/Ledger "Ledger Twitter")
  * [__](https://www.youtube.com/Ledger "Ledger Youtube")
  * [__](https://www.linkedin.com/company/ledgerhq "Ledger Linkedin company")
  * [__](https://www.tiktok.com/@ledger "Ledger Tiktok")
  * [__](https://discord.com/invite/ledger "Ledger Discord")

### Subscribe to our  
newsletter

New coins supported, blog updates and exclusive offers directly in your inbox

  

Enter your email

Register to newsletter

Your email address will only be used to send you our newsletter, as well as
updates and offers. You can unsubscribe at any time using the link included in
the newsletter.

[Learn more about how we manage your data and your
rights.](https://shop.ledger.com/pages/privacy-notice#ledger-newsletter)

[![](https://www.ledger.com/wp-content/themes/ledger-v2/public/images/ledger-
logo-long.svg)](https://www.ledger.com "Ledger")

  * English
    * This page is available in English only

Copyright © Ledger SAS. All rights reserved. Ledger, Ledger Stax, Ledger Nano
S, Ledger Vault, Bolos are trademarks owned by Ledger SAS.  
  
1 rue du Mail, 75002 Paris, France  
  
Payment methods  
![](/wp-content/uploads/2021/11/logo-paypal-s.png?v=2)  ![](/wp-
content/uploads/2021/11/logo-crypto-s.png?v=6)  ![](/wp-
content/uploads/2021/11/logo-bitpay-s.png?v=6)  
![](/wp-content/uploads/2021/11/layer1.png?v=2)  ![](/wp-
content/uploads/2021/11/logo-visa-s.png?v=2)  ![](/wp-
content/uploads/2021/11/logo-maestro-s.png?v=2)  ![](/wp-
content/uploads/2021/11/logo-mastercard-s.png?v=2)  ![](/wp-
content/uploads/2021/11/logo-cb-s.png?v=2)

  * Products
    * [Ledger Stax](https://shop.ledger.com/pages/ledger-stax)
    * [Ledger Nano X](https://shop.ledger.com/pages/ledger-nano-x)
    * [Ledger Nano S Plus](https://shop.ledger.com/pages/ledger-nano-s-plus)
    * [Compare our devices](https://shop.ledger.com/pages/hardware-wallets-comparison)
    * [Bundles](https://shop.ledger.com/#category-bundle)
    * [Accessories](https://shop.ledger.com/#category-accessories)
    * [All products](https://shop.ledger.com)
    * [Downloads](https://www.ledger.com/ledger-live)

  * Crypto Assets
    * [Bitcoin wallet](https://www.ledger.com/coin/wallet/bitcoin)
    * [Ethereum wallet](https://www.ledger.com/coin/wallet/ethereum)
    * [Cardano wallet](https://www.ledger.com/coin/wallet/cardano)
    * [XRP wallet](https://www.ledger.com/coin/wallet/ripple)
    * [Monero wallet](https://www.ledger.com/coin/wallet/monero)
    * [USDT wallet](https://www.ledger.com/coin/wallet/tether)
    * [See all assets](https://www.ledger.com/supported-crypto-assets)

  * Crypto Services
    * [Crypto Prices](https://www.ledger.com/coin/price)
    * [Buy crypto](https://www.ledger.com/buy)
    * [Staking crypto](https://www.ledger.com/staking)
    * [Swap crypto](https://www.ledger.com/swap)

  * For Business
    * [Ledger Enterprise Solutions](https://enterprise.ledger.com/)

  * For Startups
    * [Funding from Ledger Cathay Capital](https://www.ledger.com/cathay-ledger-fund)

  * For Developers
    * [The Developer Portal](https://developers.ledger.com/)

  * Get started
    * [Start using your Ledger device](https://www.ledger.com/start)
    * [Compatible wallets and services](https://www.ledger.com/ledger-wallets-and-services)
    * [How to buy Bitcoin](https://www.ledger.com/buy-bitcoin)
    * [Guide before buying bitcoin](https://www.ledger.com/buy-bitcoin/how)
    * [Bitcoin Hardware Wallet](https://shop.ledger.com/pages/bitcoin-hardware-wallet)

  * See also
    * [Support](https://support.ledger.com/hc)
    * [Bounty program](https://donjon.ledger.com/bounty/)
    * [Resellers](/reseller)
    * [Ledger Press Kit](https://www.ledger.com/press)
    * [Affiliates](https://www.ledgerwallet.com/affiliates/)
    * [Status](https://status.ledger.com/)
    * [Partners](/partners)

  * Careers
    * [Join us](https://www.ledger.com/career)
    * [All jobs](https://www.ledger.com/jobs)

  * About
    * [Our vision](https://www.ledger.com/blog/we-are-ledger-a-brand-vision)
    * [Ledger Academy](https://www.ledger.com/academy)
    * [The company](/the-company)
    * [The people](/the-people-behind-ledger)
    * [Diversity](https://www.ledger.com/diversity)
    * [Blog](/blog)

  * Legal
    * [Legal Center](https://www.ledger.com/legal-center)
    * [Sales Terms and Conditions](https://shop.ledger.com/pages/terms-and-conditions)
    * [Privacy Policy](https://www.ledger.com/privacy-policy)
    * [Disclaimers](https://shop.ledger.com/pages/disclaimers)

![](https://www.facebook.com/tr?id=237213137153741&ev=PageView&noscript=1)

## Your Cookies preferences !

We use cookies to analyse the traffic on our site, enhance your experience and
deliver marketing contents that are relevant to your interests. Please note
that you can change your cookie settings and withdraw your consent at any time
from our[Cookie Policy](https://shop.ledger.com/pages/cookie-policy)

Reject All Accept All

Cookies Settings

![Ledger Logo](https://cdn.cookielaw.org/logos/df21fb3f-71b8-491b-89ee-
eb777bcaf866/56e0a676-5d93-4a14-bfc7-7a2d75f2b993/15ffac82-5822-4def-b3b3-a595598861a2/White_64.png)

## Privacy Preference Center

  * ### Your Privacy

  * ### Strictly Necessary Cookies

  * ### Performance Cookies

  * ### Functional Cookies

  * ### Targeting Cookies

  * ### Social Media Cookies

#### Your Privacy

When you visit any website, it may store or retrieve information on your
browser, mostly in the form of cookies. This information might be about you,
your preferences or your device and is mostly used to make the site work as
you expect it to. The information does not usually directly identify you, but
it can give you a more personalized web experience. Because we respect your
right to privacy, you can choose not to allow some types of cookies. Click on
the different category headings to find out more and change our default
settings. However, blocking some types of cookies may impact your experience
of the site and the services we are able to offer.  
[More information](https://shop.ledger.com/pages/cookie-policy)

#### Strictly Necessary Cookies

Always Active

These cookies are necessary for the website to function and cannot be switched
off in our systems. They are usually only set in response to actions made by
you which amount to a request for services, such as setting your privacy
preferences, logging in or filling in forms. You can set your browser to block
or alert you about these cookies, but some parts of the site will not then
work. These cookies do not store any personally identifiable information.

View Vendor Details‎

#### Performance Cookies

Performance Cookies

These cookies allow us to count visits and traffic sources so we can measure
and improve the performance of our site. They help us to know which pages are
the most and least popular and see how visitors move around the site. All
information these cookies collect is aggregated and therefore anonymous. If
you do not allow these cookies we will not know when you have visited our
site, and will not be able to monitor its performance.

View Vendor Details‎

#### Functional Cookies

Functional Cookies

These cookies enable the website to provide enhanced functionality and
personalisation. They may be set by us or by third party providers whose
services we have added to our pages. If you do not allow these cookies then
some or all of these services may not function properly.

View Vendor Details‎

#### Targeting Cookies

Targeting Cookies

These cookies may be set through our site by our advertising partners. They
may be used by those companies to build a profile of your interests and show
you relevant adverts on other sites. They do not store directly personal
information, but are based on uniquely identifying your browser and internet
device. If you do not allow these cookies, you will experience less targeted
advertising.

View Vendor Details‎

#### Social Media Cookies

Social Media Cookies

These cookies are set by a range of social media services that we have added
to the site to enable you to share our content with your friends and networks.
They are capable of tracking your browser across other sites and building up a
profile of your interests. This may impact the content and messages you see on
other websites you visit. If you do not allow these cookies you may not be
able to use or see these sharing tools.

View Vendor Details‎

Back Button

### Vendors List

Filter Button

Consent Leg.Interest

checkbox label label

checkbox label label

checkbox label label

Clear

checkbox label label

Apply Cancel

Confirm My Choices

Allow All

[![Powered by
Onetrust](https://cdn.cookielaw.org/logos/static/powered_by_logo.svg)](https://www.onetrust.com/products/cookie-
consent/)

