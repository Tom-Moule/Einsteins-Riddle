# Einsteins-Riddle
Einstein's Riddle solved using python, pandas and pure logic

Einstein's riddle is a famous logic problem, in which there are 5 houses of unknown but fixed positions relative to each other, each with a unique colour, and each with a resident who has a unique nationality, pet, and drink and cigarette preference.

Puzzlers are given a series of insights in order to work out all the details of who lives in each house.

In this project, I develop a way to use the insights given as inputs into tailored functions, which allow me to narrow down the possible combinations for each of the houses.


## Description
My motivation for this project stems from a keen interest in logic puzzles, and a desire to develop my python skills through the process of solving definitive problems. 

My approach for solving this problem was to:
start with a master data frame with 6 columns (1 for each of position, colour, drink, pet, nationality, cigar preference), and all possible combinations of combinations as the rows. Given that each column has 5 possible values, this meant 5**6 = 15625 possible rows.
Use the insights given to remove rows that could not be part of the solution

From inspecting the insights, I first discovered that many were of the form “The Dane drinks Tea”, meaning that rows where nationality == Danish, but drink != tea could be removed; as could rows where nationality != Danish, but drink == tea.
I hence develop a function ‘reduce_using_pattern_A’ which took in the dataframe, a first variable name (i.e. nationality), a first variable value (i.e. Danish), a second variable name (i.e. drink), and a second variable value (i.e. tea). And filtered out rows that could not be part of the solution.
By using this filtering function sequentially, for each of the insights of the form “The Dane Drinks Tea” - I was able to reduce the number of potential rows from 15625 to 80.

I then inspected the remaining insights, which included: 
The Green house is exactly to the left of the White house.
The man who smokes Blends lives next to the one who keeps Cats.
The man who keeps Horses lives next to the man who smokes Dunhill.

Rather than immediately trying to develop a function that could take into account these complex relationships, I chose to first translate these insights into simpler insights, of the form:
The Green House is not House 5 (i.e. the rightmost house)
The man who smokes blends does not keep cats
I hence developed a function, reduce_using_pattern_B, that would remove, for instance, all rows where House was 5 and colour was green. This function took in data frame, a single variable and a single value as its arguments.
By using this function sequentially on all relevant insights, I was able to reduce the number of potential rows from 80 to 55. 
Following on from this, I inspected the dataset to extract further insights, and - by a hands on process that often involved reusing the two functions described above - discovered the 5 rows that had to represent the solution.
Reflecting that the final phase of the problem solving had been quite ad hoc, I chose to explore alternative ways of reducing the number of potential rows. 
I found a way to automatically identify variable-value pairs that had to co-occur - as a hypothetical example, it could find that the value of drink for Germans was always beer, and so remove any rows where other nationalities drank beer.
This function demonstrated some value, as it did allow for the number of potential rows to be reduced without further insights being added manually. However, using it sequentially did tend to result in rows to be removed being exhausted, without a final solution being reached. 



## File Structure

- Einstein's Riddle.ipynb (all data generated within file)
