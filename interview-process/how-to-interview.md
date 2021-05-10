# How To Approach Interviews

## Goals

- List the recommended steps to take in a whiteboard interview

## Introduction

Years of practice performing technical interviews have lead Ada to a process to improve candidate chances in a technical interview.  These steps describe a general approach and are useful to:

- Reduce nervousness by providing the candidate with a script to follow and practice
- Reduce the chances of misunderstanding the question
- Encourage the candidate to engage the interviewer and convey your thought process

In this lesson we will apply these steps to the following interview question:

```
Write a program to check whether a given number is an ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5.
```

## Starting the Interview

A technical interview typically starts like a general interview with introductions and a bit of discussion.

You should be prepared to talk about:

- Prior work experience
- Past projects
- Items highlighted on your resume
- Why you are excited about the position

<!-- available callout types: info, success, warning, danger, secondary  -->
### !callout-info

## This Will Sound Familiar

If this process sounds famialiar... It SHOULD!  The **P**roblem **S**olving **E**xercises you have engaged in every week are designed to help you practice the interview process!

### !end-callout

## Introduction of the Whiteboard Problem

After the introductions are concluded the interviewer will introduce the whiteboard problem(s).  Remember to let the interviewer finish providing the problem and take notes.

After the interviewer finishes the question, repeat the problem in your own words and verify that you understand the problem.

### Ask Clarifying Questions

Before starting on the solution, ask clarifying questions.  Clarifying questions can help you identify any missing bits of information needed to solve the problem, and identify requirements.

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: short-answer
* id: 50473b2b-d4fc-4d93-9c45-cb3cad358be7
* title: Sample Question & Clarifying Questions
* points: 1
* topics: Interviewing

##### !question

For the following question, identify a clarifying question.

```
Write a program to check whether a given number is an ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5.
```

##### !end-question

##### !answer

/.+/
##### !end-answer

##### !placeholder



##### !end-placeholder

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, hidden, students click to view) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation

Some clarifying questions could include:

- Does 1 count?
- Can the prime factors include a combination of 2, 3 and 5?
- Can you define prime factors?

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

### Determine Test Input-Output

The next step is to determine sample input into the problem and the resulting output.  This allows the applicant to verify how well they understand the problem and how the solution should perform.

When creating sample input-output look for edge-cases and nominal cases.  Solicit feedback from the interviewer to verify that your sample input and output values are correct and you understand the problem.

Keep the sample input and output values because they can be useful in testing the solution.

It can also be quite helpful to ask for **test cases**.  Some interviewers may provide pre-written unit tests for the problem, others may provide useful input-output examples of their own.  Candidates who ask for test cases also demonstrate a knowledge of Test Driven Development.

**Example**:

```
Write a program to check whether a given number is an ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5.

Sample #1:
Input:  21
Output: False

Sample #2
Input: 1
Output: True
```

### Describe The Approach

After developing sample input and output values, being developing a solution.  Describe the approach to the interviewer and write down the steps.  Pseudocode can be quite helpful.  Get feedback from the interviewer and listen to any questions they have.  The interviewer will often ask questions to help identify bugs in the approach or unforseen edge-cases.

**Example**

```
We will take in the sample number `num`

loop until num mod 2 is not 0
  - num = num mod 2

loop until num mod 3 is not 0
  - num = num mod 3

loop until num mod 5 is not 0
  - num = num mod 5

if num is 1 return True
Otherwise return False
```

<!-- available callout types: info, success, warning, danger, secondary  -->
### !callout-success

## Pro-Tip Use "We"

When discussing the problem a candidate should try to engage the interviewer in the process as a collaborator.  Use terms like "we" when talking abou the problem and solution.  

In general, an interviewer *wants* the candidate to succeed and by engaging in a collaborative process, you can both become more at-ease and solicit more helpful feedback.

### !end-callout

### Begin Coding

Once the candidate has discussed the approach with the interviewer and answered any questions it is time to begin coding.

While coding the solution it is important to remember to:

- Explain each step while coding
- When pausing to think, speak aloud to explain the thought process, interviewers need to understand what the candidate is thinking
- Pause regularly to test each step using the input-output values from before

Remember **communication is key**.  An interviewer needs to understand the candidate's thinking.

<!-- available callout types: info, success, warning, danger, secondary  -->
### !callout-success

## Pro Tip - Ask for Help

When stuck, there is nothing wrong with a candidate asking for help.  The interviewer could respond with, "no," but often will respond with a useful tip to get the candidate past the sticking point. 

### !end-callout

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: code-snippet
* language: python3.6
* id: 34d253f6-5369-4308-acd7-115074d10d18
* title: Ugly Number Problem
* points: 1
* topics: python, interviews

##### !question

Write a program to check whether a given number is an ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5.

```
Sample #1:
Input:  21
Output: False

Sample #2
Input: 1
Output: True
```

```py
def test_one():
    assert ugly_number(1) == True

def test_two():
  assert ugly_number(3) == True

def test_three():
  assert ugly_number(5) == True

def test_four():
  assert ugly_number(22) == False

def test_five():
  assert ugly_number(30) == True

def test_six():
  assert ugly_number(150) == False
```

##### !end-question

##### !placeholder


```py
def ugly_number(num):
  '''
  INPUT: A positive number
  OUTPUT: boolean
  '''
  pass
#   return 1
```

##### !end-placeholder

##### !tests

```py
import unittest
from main import ugly_number

class TestUglyNumber(unittest.TestCase):
  def test_one(self):
    self.assertEqual(ugly_number(1), True)

  def test_two(self):
    self.assertEqual(ugly_number(3), True)

  def test_three(self):
    self.assertEqual(ugly_number(5), True)

  def test_four(self):
    self.assertEqual(ugly_number(22), False)

  def test_five(self):
    self.assertEqual(ugly_number(30), True)

  def test_six(self):
    self.assertEqual(ugly_number(150), False)    
```

##### !end-tests

<!-- other optional sections -->
##### !hint

Sample Solution

```python
for divisor in [2, 3, 5]:
    while num % divisor == 0:
        num = num // divisor

return num == 1
```

##### !end-hint
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
<!-- !explanation - !end-explanation (markdown, students can see after answering correctly) -->

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

### Test Your Solution

When a candidate finishes programming they should test their solution with the sample input and output values and verify that the solution works.  Testing helps verify that no edge-case has been missed.

### Solution Discussion

After presenting the solution the candidate will often be expected to discuss the pros and cons of the solution as written.  Candidates should be prepared to identify the time and space complexity and talk about alternate approaches, if time allows.  Interviews can be stressful and time constrained, so a candidate may not have had time to refactor and create an ideal solution, but they can discuss what next steps they would follow.

<!-- available callout types: info, success, warning, danger, secondary  -->
### !callout-success

## Perfection is **NOT** the Goal

The goal of a good interviewer is not to see the candidate arrive at a perfect solution, even if one exists.  A perfect solution is nice, but the real goal is to understand what the candidate could bring to the team.

Interviewers want to know:

- Will this candidate respond to feedback?
- Can this candidate communicate their thoughts in a technical environment?
- Would this candidate be a good team member?
- How well does this candidate solve problems?

### !end-callout

### Interview Conclusion

At the conclusion of the interview the candidate should thank the interviewer for their time.  