# Lab 07 - Test First Programming II (Social Network Analysis)

SE-314 Software Construction - Lab 07

Name: Aryan Zia	
CMS: 505899

Solution to Problem 3 of Problem Set 1 ("Tweet Tweet") from MIT 6.005, written test-first with JUnit. This repo continues the Lab 05 work (Problems 1 and 2).

## Scope

- **Extract** (`src/twitter/Extract.java`), from Lab 05
  - `getTimespan(tweets)`: minimum-length time interval containing every tweet's timestamp.
  - `getMentionedUsers(tweets)`: set of usernames mentioned in the tweets, lowercase, each reported once.
- **Filter** (`src/twitter/Filter.java`), from Lab 05
  - `writtenBy`, `inTimespan`, `containing`.
- **SocialNetwork** (`src/twitter/SocialNetwork.java`), Lab 07
  - `guessFollowsGraph(tweets)`: infers that A follows B when A @-mentions B.
  - `influencers(followsGraph)`: all usernames in the graph, sorted by number of followers, most followed first.

## Test-first approach

For `SocialNetwork`, the tests in `test/twitter/SocialNetworkTest.java` were written before the implementation:

1. A testing strategy comment partitions the input and output space of each method.
2. Each test names the partitions it covers with a `// covers:` comment.
3. The suite was run against the stub methods (red: 10 errors, `not implemented`), then the implementations were added until all 11 tests passed (green).

The tests respect the underdetermined postcondition of `guessFollowsGraph`. They only check the follows that the spec requires, and they compare usernames ignoring case. A variant that keeps every author as a key with an empty set also passes.

## Layout

```
src/twitter/     Extract, Filter, Main, SocialNetwork, Timespan, Tweet, TweetReader
test/twitter/    ExtractTest, FilterTest, SocialNetworkTest
lib/             junit-4.13.2.jar, hamcrest-core-1.3.jar, javax.json-1.0.jar
tweets.txt       sample tweets used by Main
```

## Running

In Eclipse, right-click `SocialNetworkTest.java` and choose **Run As → JUnit Test**. Enable assertions with `-ea` in the VM arguments of the run configuration.

From a terminal (JDK 17 or later):

```
javac -d bin -cp "lib/*" src/twitter/*.java test/twitter/*.java
java -ea -cp "bin;lib/*" org.junit.runner.JUnitCore twitter.SocialNetworkTest
java -cp "bin;lib/*" twitter.Main
```

`Main` reads `tweets.txt` from the project folder. Its output lists the number of tweets, the timespan, and the top influencers.