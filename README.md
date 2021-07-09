
# PyCitySchools with Pandas - A School District Analysis

## Project Overview 
The Chief Data Scientist for a city school district, Maria, was tasked to aggregate data in order to report and show trends in school performance. This included analyzing standardized test scores for math and reading, student funding, and other school information that may be useful for the school board's planning. The goal was to provide an analysis to aid in the decision-making process of school budgets and priorities using Pandas and NumPy.

### The Challenge
According to the school board, math and reading scores of the ninth graders from Thomas High School were altered and showed evidence of academic dishonesty. To uphold state-testing standards, the challenge was to replace the scores in question with NaN (not a number) and keep the rest of the data untouched. In addition, the school district analysis was repeated and compared to the initial analysis to see how the changes affected the results.

### Resources
- Data: 
    - [Student Information](https://github.com/samanthajpv/School_District_Analysis/blob/fa909725256cc6fe437218b2fac80b0852f43f12/Resources/students_complete.csv)
    - [School Information](https://github.com/samanthajpv/School_District_Analysis/blob/fa909725256cc6fe437218b2fac80b0852f43f12/Resources/schools_complete.csv)
- Software: Python 3.8.8, Jupyter Notebook 6.3.0
- Refer to [PyCitySchools_Challenge](https://github.com/samanthajpv/School_District_Analysis/blob/5eef8e19292d6cd3a292d1803041488e4121763e/PyCitySchools_Challenge.ipynb) for the complete code.
- *Note: In accordance with [__FERPA__](https://www2.ed.gov/policy/gen/guid/fpco/ferpa/index.html), student information was strictly used for the purpose of conducting studies.*

## Results
Before analyzing the seven school district metrics, the names of the students were cleaned by removing unnecessary prefixes and suffixes. This was done to create standardization in the names of the students as required by the school board (refer to [cleaning_student_names.ipynb](https://github.com/samanthajpv/School_District_Analysis/blob/5eef8e19292d6cd3a292d1803041488e4121763e/Resources/Additional/cleaning_student_names.ipynb) for this process). The *Student Information* and *School Information* files were merged to create a new dataframe where the analysis below was based on. 

The math and reading scores of the 9th graders from Thomas High School were replaced with NaN by the code below. The ```.loc``` method, together with conditionals, were used to access the data that needed replacement. ```np.nan``` is the new value where 'np' was the alias used for NumPy and 'nan' is a constant for not a number.
```
student_data_df.loc[(student_data_df["school_name"] == "Thomas High School") & 
                    (student_data_df["grade"] == "9th"),"reading_score"] = np.nan
```
For the metrics and images below, *initial* refers to the original analysis while *updated* refers to the analysis after the grade modification.
<ul>
<li><p><b>District Summary</b>
<p align="center">
    <img src="https://github.com/samanthajpv/School_District_Analysis/blob/5eef8e19292d6cd3a292d1803041488e4121763e/Resources/Additional/District%20Summary.png" width="800" height="140" align="center">
</p>
    The only change in the district summary that was affected was the <em>Average Math Score</em>. It went down by 0.1, which is minimal. The percentages were calculated using a new student count by subtracting the number of 9th graders from Thomas High School.</p></li>

<li><p><b>School Summary</b>
<p align="center">
    <img src="https://github.com/samanthajpv/School_District_Analysis/blob/5eef8e19292d6cd3a292d1803041488e4121763e/Resources/Additional/School%20Summary.png" width="700" height="500" align="center">
</p>
The school summary for Thomas High School was affected by replacing the 9th grader scores to NaN, while the rest of the schools reported the same numbers. The updated passing percentages for the 9th-12th graders decreased drastically from above 90% to 60-70%. This is because the calculation used the original number of students which represented the whole dataset. Since there was a modification in the scores, the analysis for Thomas High School was recalculated by using only the number of students from grades 10-12. The final result was almost the same as the initial analysis. <em>Average Reading Score</em> increased by 0.05, while the math score and all passing percentages went down as seen in the decimal places.</p></li>

<li><p><b>School Performance</b>

The schools were arranged by the <em>% Overall Passing</em> and was done by the code below:

```top_schools = per_school_summary_df.sort_values(["% Overall Passing"], ascending=False)```
<p align="center">
    <img src="https://github.com/samanthajpv/School_District_Analysis/blob/5eef8e19292d6cd3a292d1803041488e4121763e/Resources/Additional/Top%205%20Performing%20Schools.png" width="700" height="400" align="center">
</p>
<p align="center">
    <img src="https://github.com/samanthajpv/School_District_Analysis/blob/e395e6aac4ba4cc5d57da3d6bfe5d135d9da9b2d/Resources/Additional/Bottom%205%20Performing%20Schools.png" width="625" height="250" align="center">
</p>
Like the School Summary, only the data for Thomas High School changed. It still was in the top 5 performing schools and retained the 2nd place. The bottom 5 performing schools did not change and was displayed in ascending order.</p></li>

<li><p><b>Math and Reading Scores by Grade</b>
<p align="center">
    <img src="https://github.com/samanthajpv/School_District_Analysis/blob/5eef8e19292d6cd3a292d1803041488e4121763e/Resources/Additional/Math%20&%20Reading%20Scores.png" width="575" height="450" align="center">
</p>
    The upated scores for the 9th graders at Thomas High School were replaced with <em>nan</em>. The scores of 83.6 and 83.7 for math and reading respectively, were the scores in question by the school board. The main reason of redoing the analysis is to preserve data integrity. Compromised data is of little to no use, can greatly affect an analysis, and can even be dangerous since business decisions are based on data <em>(Brook, 2020)</em>.</p></li>

<li><p><b>Scores by School Spending</b>

There were four bins created for the spending ranges. The ```.describe``` method was used to check the maximum and minimum per student budget where the bins were based on. ```.cut``` method was used to identify the bin for each student and afterwhich, the score averages were calculated.
```
spending_bins = [0, 585, 630, 645, 675]
group_names = ["<$584", "$585-629", "$630-644", "$645-675"]
#Categorize spending based on the bins
per_school_summary_df["Spending Ranges (Per Student)"] = pd.cut(per_school_capita, spending_bins, labels=group_names)
```

<p align="center">
    <img src="https://github.com/samanthajpv/School_District_Analysis/blob/5eef8e19292d6cd3a292d1803041488e4121763e/Resources/Additional/Scores%20by%20school%20spending.png" width="675" height="275" align="center">
</p>
The results for scores by school spending did not change at all. Thomas High School belonged to the <em>$630-644</em> bin where there was negligible change in the scores. After formatting the scores and percentages, the result was the same as the initial analysis.</p></li>
    
<li><p><b>Scores by School Size</b>
<p align="center">
    <img src="https://github.com/samanthajpv/School_District_Analysis/blob/20c52b6dc6ce38061e48b65b985d66390202dc64/Resources/Additional/Scores%20by%20school%20size.png" width="675" height="275" align="center">
</p>
The same process from the school spending was applied when creating the bins for the school size. Thomas High School belonged under the <em>Medium</em> school size category. The raw scores and percentages showed insignificant change resulting to the same numbers after the number formatting was applied.</p></li>
    
<li><p><b>Scores by School Type</b>
<p align="center">
    <img src="https://github.com/samanthajpv/School_District_Analysis/blob/20c52b6dc6ce38061e48b65b985d66390202dc64/Resources/Additional/Scores%20by%20school%20type.png" width="675" height="275" align="center">
</p>
By using only groupby and mean, the scores by school type metric was created. Only the <em>Charter</em> numbers were affected since Thomas High School is under that category. Just like the scores by school spending and school size, the scores by school type was not affected by the change. There was minimal difference in the raw output but the formatted dataframe generated the same figures.</p></li>
</ul>

## Summary
After replacing the scores of the 9th graders from Thomas High School to NaN, although difference in output is minimal, below are the changes in the school district analysis:
- The school performance of Thomas High School only represented scores from 10th-12th graders. 
- Total student count for percentage passing calculations excluded the number of 9th graders from Thomas High School.
- The District Summary *Average Math Score* decreased by 0.1.
- With the formatting of one decimal place for grades and no decimal place for passing percentages, *Average Reading Score* increased by 0.1 in the School Summary and School Performance metrics.

## Reference
    
(1) Trilogy Education Services. (2021, July). *Module 4 Challenge*. https://courses.bootcampspot.com/courses/626/assignments/13382?module_item_id=212308
    
(2) Brook, C.(2020, December 1). *What is Data Integrity? Definition, Best Practices & More*. Digital Guardian. https://digitalguardian.com/blog/what-data-integrity-data-protection-101
