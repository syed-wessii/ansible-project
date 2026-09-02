# Linux Assignment 3B – Tom, Cat and Tomcat

## Objective
Create a Bash script that accepts a number as a command-line argument and prints:

- `tomcat` if the number is divisible by 15
- `tom` if the number is divisible by 3
- `cat` if the number is divisible by 5
- The number itself if it is not divisible by 3 or 5

## File
`assignment3b.sh`

## How to Run
```bash
chmod +x assignment3b.sh
./assignment3b.sh 15
```

## Test Cases

### Divisible by 15
```bash
./assignment3b.sh 15
```


### Divisible by 3
```bash
./assignment3b.sh 9
```

### Divisible by 5
```bash
./assignment3b.sh 10
```

### Divisible by Neither 3 nor 5
```bash
./assignment3b.sh 7
```


## Complete Verification
```bash
echo "15 -> $(./assignment3b.sh 15)"
echo "9  -> $(./assignment3b.sh 9)"
echo "10 -> $(./assignment3b.sh 10)"
echo "7  -> $(./assignment3b.sh 7)"
```



## Syntax Verification
```bash
bash -n assignment3b.sh
echo $?
```
****************************************************


