# AWK Workshop

This is a short workshop for helping people to learn and use AWK in a practical way.

## Quickstart

### Clone the repo
```shell
git clone https://github.com/theoboldalex/awk_workshop.git
```

### Inspect the data
```shell
wc -l worker_bees.csv
```
```shell
head -n 1 worker_bees.csv
```
```shell
cat worker_bees.csv
```

### Work through the exercises
There are a number of exercises listed below. Solve them in any way you see fit. You don't _have_ to use AWK, but it _is_ particularly well suited for the task.
There is no wrong or right way to do this. Just use the tools you are most comfortable with, whether that is AWK, Perl, Bash or anything else. It is supposed to be fun!

> [!WARNING]
> If you accidentally (or purposefully) bork your input file, simply generate a new one by running `make`.

## Exercises

> [!NOTE]
> From here on out we will refer to `worker_bees.csv` as the "input file".

### 1. Print the number of columns contained in the input file.
<details>
    <summary>Expand Solution</summary>

#### awk
```bash
awk -F, '{print NF; exit}' worker_bees.csv
```

#### perl
```bash
perl -F, -lane 'print scalar @F; exit' worker_bees.csv
```
#### shell
```bash
head -n 1 worker_bees.csv | tr -dc ',\n' | wc -c
```
</details>

### 2. What is the higest salary of all worker bees?
<details>
    <summary>Expand Solution</summary>

#### awk
```bash
awk -F, 'NR > 1 && $7 > max {max=$7} END{print max}' worker_bees.csv
```

</details>

### 3. What is the total yearly salary of the worker bees based in France?
<details>
    <summary>Expand Solution</summary>

#### awk
```bash
awk -F, '$6 ~ /FR/ {ts+=$7} END{print ts}' worker_bees.csv
```
</details>

### 4. What is the job title of the oldest worker bee?
<details>
    <summary>Expand Solution</summary>

### awk && shell
```bash
awk -F, 'NR > 1 {print $4 " " $5}' worker_bees.csv | sort | head -n 1
```
</details>

### 5. Which country has the highest headcount?
<details>
    <summary>Expand Solution</summary>

#### awk
```bash
awk -F, 'NR > 1 {ciso[$6]++} END{for (c in ciso){print c ": " ciso[c]}}' worker_bees.csv
```
</details>

### 6. Print the full name and job title of all worker bees that have `fred` in their name. 
> [!IMPORTANT]
> Beware some worker bee names may not be all lower cased.
<details>
    <summary>Expand Solution</summary>

#### awk
```bash
awk -F, '/[fF]red/ {print $1 " " $2 " " $5}' worker_bees.csv
```
</details>

### 7. What is the most common job title for a worker bee? Print a table of all job titles and the frequency with which they appear
<details>
    <summary>Expand Solution</summary>

#### awk
```bash
awk -F, 'NR > 1 {titles[$5]++} END{for (t in titles) {print t ": " titles[t]}}' worker_bees.csv
```
</details>

### 8. How many lead developers are there working from the US?
<details>
    <summary>Expand Solution</summary>

#### awk
```bash
awk -F, '/Lead Developer/ && $7 = "US" {c+=1} END{print c}' worker_bees.csv
```
</details>

### 9. Make a new row of data right below the headers with your name and details
<details>
    <summary>Expand Solution</summary>

#### awk
```bash
awk -F, 'NR == 1 {print; print "Alex,Theobold,alex.theobold@shitpost.ing,1987-06-30,\"Scrum Master\",UK,69420"} NR > 1' worker_bees.csv > tmp && mv tmp worker_bees.csv
```
</details>

### 10. Remove any worker bees that were not born on a leap year
<details>
    <summary>Expand Solution</summary>

#### awk
```bash
echo | awk '{print "good" " " "luck!"}'
```
</details>

