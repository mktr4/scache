# SCache
[![Build Status](https://travis-ci.org/evolution-gaming/scache.svg)](https://travis-ci.org/evolution-gaming/scache)
[![Coverage Status](https://coveralls.io/repos/evolution-gaming/scache/badge.svg)](https://coveralls.io/r/evolution-gaming/scache)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/d6da847f1228485e91525112112fb86b)](https://www.codacy.com/app/evolution-gaming/scache?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=evolution-gaming/scache&amp;utm_campaign=Badge_Grade)
[![version](https://api.bintray.com/packages/evolutiongaming/maven/scache/images/download.svg) ](https://bintray.com/evolutiongaming/maven/scache/_latestVersion)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellowgreen.svg)](https://opensource.org/licenses/MIT)

## Key features

* Load value if missing
* Expiry of not used records
* Does not exceed max size
* Tagless Final 

## Api 

```scala
trait Cache[F[_], K, V] {

  def get(key: K): F[Option[V]]

  def getOrUpdate(key: K)(value: => F[V]): F[V]

  /**
    * @return previous value if any, possibly not yet loaded
    */
  def put(key: K, value: V): F[Option[F[V]]]

  def keys: F[Set[K]]
  
  /**
    * Might be an expensive call
    */
  def values: F[Map[K, F[V]]]

  /**
    * @return previous value if any, possibly not yet loaded
    */
  def remove(key: K): F[Option[F[V]]]

  def clear: F[Unit]
}
```

## Setup

```scala
resolvers += Resolver.bintrayRepo("evolutiongaming", "maven")

libraryDependencies += "com.evolutiongaming" %% "scache" % "0.0.1"
```