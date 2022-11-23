https://stackoverflow.com/questions/ask

Antlr4 Python target broken - contains C++ code

I want to parse SparkSql code in python3. The spark sql grammar can be found here:
https://github.com/apache/spark/tree/master/sql/catalyst/src/main/antlr4/org/apache/spark/sql/catalyst/parser

I grabbed pre-built antlr4 jar version 4.11.1 from here https://www.antlr.org/download.html
I installed java version 19.0.1.

I ran the antlr4 tool:

```
java -cp C:\dev\antlr4\antlr-4.11.1-complete.jar org.antlr.v4.Tool -o out -Dlanguage=Python3 .\SqlBaseLexer.g4 .\SqlBaseParser.g4
```

When I inspect the file `SqlBaseLexer.py` that was generated it is not valid python.  For example, it contains the following section with the function `isHint` missing in the rest of the file. 

```
/**
 * This method will be called when we see '/*' and try to match it as a bracketed comment.
 * If the next character is '+', it should be parsed as hint later, and we cannot match
 * it as a bracketed comment.
 *
 * Returns true if the next character is '+'.
 */
public boolean isHint() {
  int nextChar = _input.LA(1);
  if (nextChar == '+') {
    return true;
  } else {
    return false;
  }
}
```
(see the full file in my repo here https://github.com/mrmasterplan/sparksqlparser/blob/main/src/sparksqlparser/grammar/out/SqlBaseLexer.py#L1838
)

This is not valid python. 

I can of course try to fix the file myself, but I think it would be nicer if antlr4 actually generated valid python.


I tried to use antlr4 to generate a parser for SparkSql.
I expected antlr4 to generate python code that was able to parse SparkSql.
The files the antlr4 generated were not valid python.

antlr antlr4 python python-3.x apache-spark

