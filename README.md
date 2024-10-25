# Mez Validation Library
It is a pure and open source node js library that provides validation method to check from inputs and thier data

# First lunch
2024-10-25

# Installation
npm install --save mez-validaton

# How it works?
After install this library yuo just have to select the language wich you want to show messages by it, then you have to call validation method to enter the data

# Valid languages
EN => english (default)
AR => arabic

## Ex1:
    const age = 10;

    Mez.lang("AR") // langauge of messages will shown in arabic

    Mez.validation([
    {
        name: "age",
        data: age,
        is: ["required", "number", "less:15"]
    }
    ])

=> value will return: 

    {
        messages: [],
        error: false,
        check: [
            { title: 'age', task: 'required', pass: true },
            { title: 'age', task: 'number', pass: true },
            { title: 'age', task: 'less', pass: true },
        ],
        wrongInputs: [],
        status: 200
    }

## Ex2:
    const age = 10;

    Mez.validation([
    {
        name: "age",
        data: age,
        is: ["required", "string"]
    }
    ])

=> value will return: 

    {
        messages: ["age must be string"], // default language is "English"
        error: true,
        check: [
            { title: 'age', task: 'required', pass: true },
            { title: 'age', task: 'string', pass: false },
        ],
        wrongInputs: [ "age" ],
        status: 400
    }

# Messages array
It provides a list of messages to be displayed when validation fails in task related in an input

# Error value
If all tasks is passed in check array => error: false, status: 200, if one task or more is not passed in check array => error: true, status: 400   

# Check array
It will ensure to check on all data and all tasks if passed or no and to handle your messages if you want

# WrongInputs array
It will contains a list of variables name which not passed in check array

# Status value 
- 200: Success (all tasks are passed in check array)
- 400: Error (there one task or more is not passed in check array)
- 401: Syntax error (there are error in enter types on data in validation or lang methods)

# How can i use Mez.Validation method?
    const age = 10;

    const validation = Mez.validation([
    {
        name: "age",
        data: age,
        is: ["required", "string"]
    }
    ])

    if(validation.error) {
        conosole.log({state: 'falied', wrongInputs: validation.wrongInputs})
    } else {
        conosole.log({state: 'success'})
}

## NOTE: if you not insert a name to the data, it will take an default name which depaned on his index in inputs 

## Ex:

    const validation = Mez.validation([
    {
        data: age, // Default name: Input1 
        is: ["required", "string"]
    }
    ])

## NOTE: all of these patterns will return status: 401, with error message on synatx error

- 

        Mez.validation()

- 

        Mez.validation([
        {
            is: ["required", "string"]
        }
        ])

-

    Mez.validation([
    {
        data: age,
    }
    ])

# Valid Types to check in is array 
- 'required' => data must be required and can not be empty or null
- 'string' => type of data must be a string
- 'number' => type of data must be a number
- 'boolean' => type of data must be a boolean
- '[string]' => type of data must be a string array (all elements of array must be string)
- '[number]' => type of data must be a number array (all elements of array must be number)
- '[boolean]' => type of data must be a boolean array (all elements of array must be boolean)
- 'array' => type of data must be an array
- 'email' => data must be have a valid email format
- 'url' => data must be have a valid email format
- 'date' => data must be have a valid data format depending on (YYYY-MM-DD)
- 'time' => data must be have a valid time format depending on (HH:MM:SS)
- 'phone' => data must be have a valid phone format
- 'eq:X' => data must be equal X value (X must be selected by the developer)
- 'len:X' => length of data must be equal X value (X must be selected by the developer)
- 'max:X' => length of data must be equal or less than X value (X must be selected by the developer)
- 'min:X' => length of data must be equal or greater than X value (X must be selected by the developer)
- 'less:X' => data must be less than X value (X must be selected by the developer)
- 'more:X' => data must be greater thanX value (X must be selected by the developer)
- 'less-eq:X' => data must be equal or less than X value (X must be selected by the developer)
- 'more-eq:X' => data must be equal or greater than X value (X must be selected by the developer)
- 'not-eq:X' => data can not be equal X value (X must be selected by the developer)
- 'contains:X' => data must be contains X value (X must be selected by the developer)
- 'not-contains:X' => data can not be contains X value (X must be selected by the developer)
- 'in:X' => data must be has X value (X must be selected by the developer) #NOTE: this data must be an array to implement the in task
- 'not-in:X' => data can not be has X value (X must be selected by the developer) #NOTE: this data must be an array to implement the in task
