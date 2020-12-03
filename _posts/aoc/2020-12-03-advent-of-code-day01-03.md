---
layout: post
title: "Advent Of Code - Day01 - Day03"
preview: "Advent of Code is an Advent calendar of small programming puzzles for a variety of skill sets and skill levels."
image: /assets/images/personal/aoc0103.jpg
date: 2020-12-03 18:10:12 +0300
categories: java
---

Advent of Code is an Advent calendar of small programming puzzles for a variety of skill sets and skill levels.

I've started this challenge to improve my algorithms and data structure skills. I will not be competing to get there first, but to write efficient and elegant solutions. I am experimenting with new Java features, using Java 15 with preview features.

The challenges are structures in 2 parts, where the second one expands the complexity of the first problem. This creates the opportunity to refactor the first implementation to support both parts of the challenge. 

I've decided to do some refactoring and better structure my project:
* extracted common functionalities into the Challenge interface
``` java
public interface Challenge<T, U> {
    void solve(String inputPath);
    U partA(T input);
    U partB(T input);
}
```
* converted the Main challenge classes to one that solves all of the challenges
``` java
    public static void main(String[] args) {
        var challenges = List.of(new Day01Challenge(),
                new Day02Challenge(),
                new Day03Challenge());
        for (int i = 0; i < challenges.size(); i++) {
            challenges.get(i).solve(getPath(i + 1));
        }
    }

    private static String getPath(int day) {
        return FILE_PATH +
                DAY +
                (day < 10 ? "0" + day : day) +
                FILE_EXT;
    }
```
* converted to a maven project for easy dependency management
* TDD (test driven development) where I will start the challenge with writing the test using the AOC challenge example's input and output

Check out my solutions [advent-of-code-2020](https://github.com/BogdanAdrian11/advent-of-code-2020)