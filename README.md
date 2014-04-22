## Monocle
### Description
Monocle is a Scala lens library greatly inspired by Haskell [Lens](https://github.com/ekmett/lens).
### Build
[![Build Status](https://api.travis-ci.org/julien-truffaut/Monocle.png?branch=master)](https://travis-ci.org/julien-truffaut/Monocle)
### Usage
#### Lens
 ```scala
  case class Location(_x: Int, _y: Int)
  case class Character(_name: String, _health: Int, _location: Location)

  import monocle.Macro

  val health   = Macro.mkLens[Character, Int]("_health")
  val location = Macro.mkLens[Character, Location]("_location")
  val x        = Macro.mkLens[Location, Int]("_x")

  val barbarian = Character("Krom" , 30, Location(8,13))

 health.get(barbarian) == 30
 health.set(barbarian, 32)       == Character("Krom" , 32, Location(8,13))
 health.modify(barbarian, _ + 1) == Character("Krom" , 31, Location(8,13))

 (location compose x).set(barbarian, 0) == Character("Krom" , 31, Location(0,13))
```
#### Sub Projects
Core contains the main library concepts: Lens, Traversal, Prism, Iso, Getter and Setter.
Core only depends on [scalaz](https://github.com/scalaz/scalaz) for type classes and [scalacheck](http://www.scalacheck.org/) to encode laws.

Generic is an experiment to provide highly generalised Lens and Iso using HList from [shapeless](https://github.com/milessabin/shapeless).
Generic focus is on neat abstraction but that may come at additional runtime or compile time cost.

Example shows how other sub projects can be used.

```scala
resolvers ++= Seq(
  "Sonatype OSS Releases"  at "http://oss.sonatype.org/content/repositories/releases/",
  "Sonatype OSS Snapshots" at "http://oss.sonatype.org/content/repositories/snapshots/"
)

libraryDependencies ++= Seq(
  "com.github.julien-truffaut"  %%  "monocle-core"  % "0.1" // or 0.2-SNAPSHOT
)
```
#### Contributor Handbook
We are happy to have as many people as possible contributing to Monocle.
Therefore, we made this small workflow to simplify the process:

1.   Select or create an issue (issues tagged with label "padawan-friendly" are designed for Scala novice)
2.   Comment on the issue letting everyone knows that you are working on it.
3.   Fork Monocle
4.   Work on your fork until you are satisfied (label your commits with issue number)
5.   Submit a [pull request](https://help.github.com/articles/using-pull-requests)
6.   We will review your pull request and merge it back to master

If you have any questions, we have irc channel on [freenode](http://webchat.freenode.net/) #scala-monocle

Thank you for you contribution!
### Contact
Julien Truffaut -<br>
Ross Huggett - ross.huggett@gmail.com / [@rosshuggett](http://twitter.com/rosshuggett "@rosshuggett") </a><br>
### Version
0.1<br>
### Release Date
March 2014<br>
### Requirements
Scala 2.10.2 and SBT 0.13.<br>
