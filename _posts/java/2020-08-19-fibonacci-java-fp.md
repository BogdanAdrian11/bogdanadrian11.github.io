---
layout: post
title: "Generate a fibonacci sequence"
preview: "Generate a fibonacci sequence as long as a condition is met."
image: /assets/images/unsplashed/fibonacci.jpg
date: 2020-08-19 18:50:31 +0300
categories: java
---

Generate a fibonacci sequence as long as a condition is met. There are many ways to write a fibonacci algorithm, but today we are doing it with Java functional programming.

```java
public static void generateFibonacci(Predicate<int[]> hasNext) {
	Stream.iterate(new int[] {0, 1}, hasNext,
                   c -> new int[]{c[1], c[0] + c[1]})
			.map(f -> f[0])
			.forEach(System.out::println);
}
```
The code snippet is written with Java 11 Stream API.