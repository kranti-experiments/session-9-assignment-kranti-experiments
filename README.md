# Session 9: NamedTuples
namedtuple() is a class inside collections() module that helps to write the code more Pythonic way (to handle tuples) <br/>
namedtuple() assigns meaning to each position in tuple and offers more readable coding <br/>

The following shows how a namedtuple can be created <br/>
```bash
Example 1:
Student = namedtuple('Student', 'name course roll_number')
The RHS statement creates a namedtuple called 'Student' with the fields: name, class, roll_number

Using the above 'Student' multiple students details can be constructed like below
st1 = Student('rohan', 'epai3', 101)
st2 = Student('shravan', 'epai3', 102)
st3 = Student('zoheb', 'epai3', 103)

The fields can be accessed as
st1.name -> rohan
st1.roll_number -> 101
st2.class -> epai3
```
The following showcases the basic usage of namedtuple: <br/>
1. Instantiate with positional/keyword arguments <br/>
```bash
Student = namedtuple('Student', 'name course roll_number')
st1 = Student(name='rohan', course='epai3', roll_number=101)
st2 = Student('shravan', 'epai3', roll_number=101)
```
2. Indexable (like other iterables(list/tuples etc)) <br/>
```bash
>> st1[0]
rohan
>> st1[0] + ' ' + st2[0]
rohan shravan
```
3. Unpack (like a normal tuple) <br/>
```bash
>> student_name, student_course, student_roll_number = st1
>> student_name, student_course, student_roll_number
rohan, epai3, 101
```
4. Access the fields by name <br/>
```bash
>> st1.name + ' ' + st2.name
rohan shravan
```
5. Readable with name = value style <br/>
```bash
>> st1
Student(name='rohan', course='epai3', roll_number=101)
```

The operartors that can be used with namedtuple are: <br/>
1. _fields: Lists out the various attributes/fields of the namedtuple <br/>
In the above code snippet(Example1), st3._fields returns name, class, roll_number <br/>

2. _source: Lists out the source code for the namedtuple

3. _replace: To replace the values of fields in a namedtuple <br/>
```bash
>> st1 = Student(name='rohan', course='epai3', roll_number=101)
>> st1._replace(name='zoheb')
Student(name='zoheb', course='epai3', roll_number=101)
```

4. _asdict: Converts the named tuple to dictionary <br/>
```bash
st1 = Student('rohan', 'epai3', 101)
st1_dict = st1._asdict

type(st1) -> __main__.Student
type(st1_dict) -> collections.OrderedDict
```

Advantages of namedtuples over other dictionaries <br/>
1. Wherever tuples are used and need better readable/documented code, go for namedtuples <br/>
2. Useful for handling large csv/databases where indexing becomes messy and beneficial to have named attributes
3. Lighter weight than dictionaries, yet maintains order like dictionary <br/>

Other things to consider while using namedtuples <br/>
1. Like tuples, namedtuples are also immutable, meaning once created, new fields cannot be added
```bash
Student = namedtuple('Student', 'name course roll_number')
st1 = Student('rohan', 'epai3', 101)
>> st1.marks = 90
Unlike dictionary, new attributes cannot be created and assigned dynamically
```
## Assignment
1. Use the Faker (Links to an external site.)library to get 10000 random profiles. Using namedtuple, calculate the largest blood type, mean-current_location, oldest_person_age, and average age (add proper doc-strings). - 250 (including 5 test cases) <br/>
2. Do the same thing above using a dictionary. Prove that namedtuple is faster. - 250 (including 5 test cases) <br/>
3. Create fake data (you can use Faker for company names) for imaginary stock exchange for top 100 companies (name, symbol, open, high, close). Assign a random weight to all the companies. Calculate and show what value the stock market started at, what was the highest value during the day, and where did it end. Make sure your open, high, close are not totally random. You can only use namedtuple. - 500  (including 10 test cases) <br/>

## Functions Overview

#### generate_profiles() <br/>
This is a function to generate random(fake) profiles for given number of persons <br/>
The function uses getfaker_obj() and getfaker_profile() to generate 'Profile' and repeat the same for given number of persons and returns the list of 'Profiles' to the caller

### timed() <br/>
This is a decorator factory used for computing the average running time of a given function <br/>
This is a parameterized decorator which takes the number of repeatitions as input argument and run the function for the given number of times <br/>
This is used to compute the time taken by namedtuple and dictionary functions and compare which is faster, which is slower, which is best among them <br/>

### create_stock_exchange() <br/>
This is a function for creating dummy stock exchange <br/>
The function takes input for the number of stocks to be generated. <br/>
Optionally the stock values, weights can be pre-loaded via this function <br/>
The function returns the generated stocks and their associated weights to the caller <br/>
stocks: a list of namedtuples of type 'Stock' <br/>
'Stock': A namedtuple containing the information of a stock such as: name symbol open high close <br/>
weights: a list of (random) weights for each stock in the stock exchange <br/>

## Utility Functions
#### getfaker_obj() <br/>
This is a function to create an instance for the 'faker' class <br/>
'faker' is a third party python library to generate fake data required for simulations <br/>
Before using the library, its object has to be created and used subsequently to generate various types of fake data <br/>
The library has a provision to set seed value before the simulation so that same values gets generated in each run and easy for testing <br/>

#### getfaker_profile() <br/>
This is a function to create a fake profile for a person <br/>
The profile contains information such as name, gender, job, current location, residence, address, blood group, birthdate, email and many more <br/>
'Age' is not available by default in the faker profile and has to be computed seperately <br/>
For simplification purpose, the difference between today [when ever the functions runs, that day is treated as today] and the birthdate are computed as 'age'
As not all the values of the profile are interested for the assignment, only the values blood group(type), current location, age are wrapped in a namedtuple (Profile) and returned to the caller

### calc_time_nt_largest_blood_group() <br/>
### calc_time_dict_largest_blood_group() <br/>
This function returns the most common occuring/largest blood type in the given profiles

### calc_time_nt_mean_current_location() <br/>
### calc_time_dict_mean_current_location() <br/>
This fucntion computes the average/mean current location for the given profiles

### calc_time_nt_oldest_average_age() <br/>
### calc_time_dict_oldest_average_age() <br/>
This function computes the oldest age, average/mean age from the given profiles and returns the same


### nt_field_access() <br/>
### dict_field_access() <br/>
These functions access fields from the namedtuple/dictionary objects and used for comparing the average time taken to perform these operations for namedtuples and dictionary classes

### nt_size_compare() <br/>
### dict_size_compare() <br/>
These functions access memory occupied by the namedtuple/dictionary objects and used for comparing the average size taken to perform these operations for namedtuples and dictionary classes

### nt_instance_compare() <br/>
### dict_instance_compare() <br/>
These functions compare two instances of namedtuple/dictionary and used for comparing the average time taken to perform these operations for namedtuples and dictionary classes

### nt_unpacking() <br/>
### dict_unpacking() <br/>
These functions unpack values from the objects of namedtuple/dictionary and used for comparing the average time taken to perform these operations for namedtuples and dictionary classes

### nt_create_new_instance() <br/>
### dict_create_new_instance() <br/>
These functions create new instances of namedtuple/dictionary and used for comparing the average time taken to perform these operations for namedtuples and dictionary classes

### nt_create_new_instance() <br/>
### dict_create_new_instance() <br/>
These functions create new instances of namedtuple/dictionary and used for comparing the average time taken to perform these operations for namedtuples and dictionary classes

#### calc_open_value() <br/>
This is a function to compute the market opening value <br/>
Uses the 'open' value for each stock and by multiplying with its weight gives today's market opening value <br/>

#### calc_high_value() <br/>
This is a function to compute the market highest peak value <br/>
Uses the 'high' and 'open' values of each stock, the difference multiplied with its weights gives market high peak value <br/>

#### calc_close_value() <br/>
This is a function to compute the market closure value <br/>
Uses the 'close' and 'open' values of each stock, the difference multiplied with its weights gives market closure value <br/>

#### get_market_momentum() <br/>
This is a function to track the momentum of the stock market <br/>
It takes input as list of stocks and their associated weights <br/>
Using close, open values for each stock, computes their difference and multiply with its weight and generate the current market value <br/>
By computing the difference between current value and opening value gives an idea of market movement <br/>
If the difference is positive, then market is gaining(some/many/all stocks gain) and going upwards else it is in loss/loosing(some/many/all stocks loose) its momentum <br/>