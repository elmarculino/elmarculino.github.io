+++
title = "Bash Script Snippets"
author = ["Marco Ribeiro"]
date = 2022-10-06
draft = false
+++

## Cut string {#cut-string}

```bash
my_filename="interesting-text-file.txt"
echo ${my_filename:0:21}

echo ${my_filename%.*}

complicated_filename="hello-world.tar.gz"
echo ${complicated_filename%%.*}

echo ${my_filename/.*/}

sed 's/[.].*//' <<< 'hello-world.tar.gz'

cut -f1 -d"." <<< 'hello-world.tar.gz'
```


## ~/execute_string.sh {#execute-string-dot-sh}

```bash

your_command_string="..."
output=$(eval "$your_command_string")
echo "$output"
```


## ~/random.sh {#random-dot-sh}

```bash
echo $(( $RANDOM % 50 + 1 ))

numero=${RANDOM:0:2}
```


## ~/return_values.sh {#return-values-dot-sh}

```bash

my_function () {
  func_result="some result"
}

my_function
echo $func_result
```


## ~/return_values.sh {#return-values-dot-sh}

```bash

my_function () {
  local func_result="some result"
  echo "$func_result"
}

func_result="$(my_function)"
echo $func_result
```


## ~/passing_arguments.sh {#passing-arguments-dot-sh}

```bash

greeting () {
  echo "Hello $1"
}

greeting "Joe"
```


## if, elif, else: {#if-elif-else}

```bash

echo -n "Enter a number: "
read VAR

if [[ $VAR -gt 10 ]]
then
  echo "The variable is greater than 10."
elif [[ $VAR -eq 10 ]]
then
  echo "The variable is equal to 10."
else
  echo "The variable is less than 10."
fi
```


## Multiple conditions {#multiple-conditions}

```bash
if [[ $VAR1 -ge $VAR2 ]] && [[ $VAR1 -ge $VAR3 ]]
then
  echo "$VAR1 is the largest number."
elif [[ $VAR2 -ge $VAR1 ]] && [[ $VAR2 -ge $VAR3 ]]
then
  echo "$VAR2 is the largest number."
else
  echo "$VAR3 is the largest number."
fi
```


## Test Operators {#test-operators}

-   -n VAR - True if the length of VAR is greater than zero.
-   -z VAR - True if the VAR is empty.
-   STRING1 = STRING2 - True if STRING1 and STRING2 are equal.
-   STRING1 != STRING2 - True if STRING1 and STRING2 are not equal.
-   INTEGER1 -eq INTEGER2 - True if INTEGER1 and INTEGER2 are equal.
-   INTEGER1 -gt INTEGER2 - True if INTEGER1 is greater than INTEGER2.
-   INTEGER1 -lt INTEGER2 - True if INTEGER1 is less than INTEGER2.
-   INTEGER1 -ge INTEGER2 - True if INTEGER1 is equal or greater than INTEGER2.
-   INTEGER1 -le INTEGER2 - True if INTEGER1 is equal or less than INTEGER2.
