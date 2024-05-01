# Prototype of Measure Tracker front end

2 components: 
- Survey Creator: Drag & Drop UI to build the measure tracker's surface as a form. The form shall be stored as a JSON in a DB (e.g.MongoDB). Tutorial Drag&Drop: https://youtu.be/-kZLD40d-tI?si=tvzd_h2J8eMhHzQX
- Survey: Loads form in JSON format from database and renders it. The user can fill the survey and submit it. The result from the survey can be extracted as JSON and send to a database service. (SurveyJS FormBuilder: https://surveyjs.io/form-library)

## Project setup

```
npm install
```

## Compile and hot-reload for development

```
npm run dev
```