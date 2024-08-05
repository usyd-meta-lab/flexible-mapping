# Flexible-Mapping
Flexible Mapping Task

**Readme not updated for newest version that uses drag and drop**

![alt text](http://cogflex.com.au/users/kit/demo/ID/FM-main/screenshot.png)


## Parameters

This plugin accepts the following parameters. Parameters with a default value of undefined must be specified.


| Parameter     | Type          | Default Value | Description
| ------------- | ------------- |------------- | ------------- |
| type          | string  | undefined        | Defines the trial type. Should be set to 'flexible-map'|
| stimulus| string | undefined | The stimulus that is displayed |
| choices | array | undefined | An array of pngs to displayed as response options |
| button_text | sting | undefined | Text shown on button
| prompt | function | undefined | A function to score the response |


## Timeline Variables

Timeline variables are used to iterate across stimuli. The following timeline variables are included.

| Variable     |  Description | Example
| ------------- | ------------- |------------- |
|stimulus | the prompt shown at the top | "assets/img/prompt_1.png"
|choice1 | the first option | "assets/img/choice_1_1.png"
|choice2 | the second option | "assets/img/choice_1_2.png"
|choice3 | the third option | "assets/img/choice_1_3.png"
|choice4 | the fourth option | "assets/img/choice_1_4.png"



## Example

There are multiple trial types you can edit in the editable paramaters file. The 'map_trial' variable is the main flexible mapping trial described above.
A working demonstration can be viewed at http://cogflex.com.au/users/kit/demo/ID/FM-main/exp-demo.html
```javascript
// Stimuli and trial info
  var test_stimuli = [
    { stimulus: "assets/img/prompt_1.png", choice1: 'assets/img/choice_1_1.png', choice2: 'assets/img/choice_1_2.png' , choice3: 'assets/img/choice_1_3.png' , choice4: 'assets/img/choice_1_4.png', correct_response: 1, feedback: "The correct answer is x because xyz"},
    { stimulus: "assets/img/prompt_2.png", choice1: 'assets/img/choice_2_1.png', choice2: 'assets/img/choice_2_2.png' , choice3: 'assets/img/choice_2_3.png' , choice4: 'assets/img/choice_2_4.png', correct_response: 3, feedback: "The correct answer is \y because xyz" }
  ];



// Trial details
  var map_trial = {
      type: 'flexible-map',
      stimulus: jsPsych.timelineVariable('stimulus'),
      choices: [jsPsych.timelineVariable('choice1'),jsPsych.timelineVariable('choice2'),jsPsych.timelineVariable('choice3'),jsPsych.timelineVariable('choice4')],
      margin_vertical: "8px",
      margin_horizontal: "8px",
      response_ends_trial: true,
      on_finish: function(data){
   if(data.response + 1 == jsPsych.timelineVariable('correct_response')){
     data.correct = true;
   } else {
     data.correct = false;
   }
 }
  };

  // Timeline - include CR and feedback if desired
  var test_procedure = {
    timeline: [CR_trial, map_trial, feedback],
    timeline_variables: test_stimuli
  }
```
