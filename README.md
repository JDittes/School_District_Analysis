# School_District_Analysis
Module 4 Project in Vandy Data Bootcamp

## Overview of the school district analysis:
I was hired to assist Maria, the chief data scientist for a large school district, to analyze high school testing data. I focused on two particular areas: student test scores in math & reading, as well as and school funding.

Data is a key element of instruction. For administrators and regulators, it is a measure of the effectiveness of school & district policies. For school board members, it can help to set funding priorities. 

Unfortunately, the emphasis on testing as a SOLE metric has led to falsified scores in districts across the country. This appears to be the case at Thomas High School, where 9th-grade reading and math scores show signs of fraud. I need to nullify the 9th-grade scores at Thomas High to get an accurate look at key district indicators.

## Results:
After nullifying the 9th-grade reading scores in the challenge. These were the effects on the seven school district metrics.
- Total Students: As I analyze the data, I needed two student counts. 
  - I needed to keep the number of students in the district constant for the purposes of determining school size and funding needs, but I needed to determine a __new_student_count__ to maintain the accuracy of my math, reading, and overall test scores. 
  - This also led to the creation of two dataframes:
    __district_summary_df__ was the DataFrame I developed to recalculate the averages, excepting the 9th-grade students at Thomas High. This allowed me to have an accurate list of test scores.
  __school_data_complete_df__ was the DataFrame I developed that still included the THS 9th-graders for budget, and school-type reports.
  -  I calculated this by using __.loc__ to identify the number of 9th-graders who tested at Thomas High School: `school_data_complete_df.loc[(school_data_complete_df['grade'] == '9th') & (school_data_complete_df['school_name'] == 'Thomas High School')].count()` 
  -  This gave me a total of 461 9th-graders (__THS_count_9__) which I subtracted from __student_count__ to compute a 'clean' number of students to compile correct test scores: `new_total_student = student_count - THS_count_9`
- Total Budget: This rate was unaffected by the nullified scores
- Average Math Score: 
  - I had to adjust the math scores to reflect the nullified data from Thomas High School. 
  - I started by calculating the number of 10th-12th-graders. I did this by using __.loc__ to find every student at THS not in (__!=__) 9th grade: `THS_10_12 = school_data_complete_df.loc[(school_data_complete_df['grade'] != '9th') & (school_data_complete_df['school_name'] == 'Thomas High School'),:].count()`
  - I calculated the number of students passing math at THS: `THS_passing_math = school_data_complete_df.loc[(school_data_complete_df['school_name'] == 'Thomas High School') 
                                               & (school_data_complete_df['math_score'] >= 70)]`
  - Finally, I divided the new total by the total of 10th-12th graders: `THS_math_percentage = THS_passing_math['Student ID'].count() / THS_10_12 * 100
THS_math_percentage[0]`
- Average Reading Score: I used the same approach as described above for average math scores, except I used the data in the __THS_passing_reading__ variable.
- % Passing Math
  - I calculated the number of students passing math at THS: `THS_passing_math = school_data_complete_df.loc[(school_data_complete_df['school_name'] == 'Thomas High School')` 
  - Next I replaced the 9th-grade scores in the __per_school_summary_df__ with the average percentage for 10th-12th-graders using a for loop: `for value in THS_math_percentage:
    per_school_summary_df['% Passing Reading'] = per_school_summary_df['% Passing Reading'].replace(value)`
- % Passing Reading: I used the same approachs as described in *% Passing Math* for average reading scores, except I used the __THS_reading_percentage__ variable.
- % Overall Passing: I used the same approachs as described in *% Passing Math* for average reading scores, except I used the __THS_overall_percentage__ variable.

## Summary:

There is a statement summarizing four changes to the school district analysis after reading and math scores have been replaced (5 pt).

