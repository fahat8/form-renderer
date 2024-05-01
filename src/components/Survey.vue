<script setup lang="ts">
import 'survey-core/defaultV2.min.css';
import { Model } from 'survey-core';

// const SURVEY_ID = 1;

const surveyJson = {
  // Create multiple pages 
  "pages": [
    {
      "name": "page1",
      "elements": [
        {
          "type": "checkbox",
          "name": "car",
          "title": "Which is the brand of your car?",
          "description": "If you own cars from multiple brands, please select all of them.",
          "isRequired": true,
          "choices": [
            "Ford",
            "Vauxhall",
            "Volkswagen",
            "Nissan",
            "Audi",
            "Mercedes-Benz",
            "BMW",
            "Peugeot",
            "Toyota",
            "Citroen"
          ],
          "separateSpecialChoices": true,
          "showOtherItem": true,
          "showNoneItem": true,
          "colCount": 2,
          "showSelectAllItem": true
        },
        {
          "type": "text",
          "name": "question3"
        },
        // By using panels we can create a grid or place components in one row
        {
          "type": "panel",
          "name": "panel1",
          "elements": [
            {
              "type": "checkbox",
              "name": "question4",
              "choices": [
                "Item 1",
                "Item 2",
                "Item 3"
              ]
            }
          ],
          "startWithNewLine": false
        }
      ]
    },
    {
      "name": "page2",
      "elements": [
        {
          "type": "dropdown",
          "name": "question1",
          "choices": [
            "Item 1",
            "Item 2",
            "Item 3"
          ]
        },
        {
          "type": "text",
          "name": "question2"
        }
      ]
    }
  ],
  "showQuestionNumbers": "off"
}

const alertResults = (sender: any) => {
  const results = JSON.stringify(sender.data);
  alert(results);
  // saveSurveyResults(
  //   "https://your-web-service.com/" + SURVEY_ID,
  //   sender.data
  // )
}


const survey = new Model(surveyJson);
survey.onComplete.add(alertResults);

// function saveSurveyResults(url: string | URL, json: object) {
//   fetch(url, {
//     method: 'POST',
//     headers: {
//       'Content-Type': 'application/json;charset=UTF-8'
//     },
//     body: JSON.stringify(json)
//   })
//   .then(response => {
//     if (response.ok) {
//       // Handle success
//     } else {
//       // Handle error
//     }
//   })
//   .catch(error => {
//     // Handle error
//   });
// }
</script>

<template>
  <SurveyComponent :model="survey" />
</template>