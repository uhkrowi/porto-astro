---
layout: "../../layouts/BlogPost.astro"
title: "Generate PDF with PDFMake"
pubDate: "Mar 09, 2022"
---

In this personal site I decided to generate my CV myself rather than taking up from URL of another website (e.g you could get generated CV from [kalibrr.com](https://uhkrowi.github.io/generate-pdf-with-pdfmake/)).

In my previous project I did the job, generating pdf of documents is pretty simple, there’re some packages you could use out there, one of them is PDFmake.

PDFmake is a package that helps you to generate PDF for server-side and client-side usage in pure JavaScript (read its documentation [here](http://pdfmake.org/)), it’s a powerful tool yet easy to use, it has a [playground](http://pdfmake.org/playground.html) too for you to try it online.

Let’s get some actions.

We’ll create a PDF document of curriculum vitae that includes data of work experiences, skills and interests. To achieve that we have to provide the data and install PDFmake package first.

...

### **Providing Data**
```javascript
const experiences = [
  {
    position: "Back End Web Developer",
    company: "ABCD Company",
    date: "Dec 2021 – Current",
    jobs: ["Do something", "Do something else", "Doing it again"]
  },
  {
    position: "Front End Web Developer",
    company: "EFG Company",
    date: "Jan 2021 – Dec 2021",
    jobs: ["Do something", "Do something else", "Doing it again"]
  }
];

const skills = [
  "Javascript",
  "NodeJS",
  "React.js",
  "Vue.js",
  "PostgreSQL",
  "MongoDB"
];

const interests = [
  "Programming",
  "Web Design"
];
```

### **Install the package**
```shell
npm i pdfmake
```

### **Import the package into your project**
```javascript
import pdfMake from "pdfmake/build/pdfmake";

// if there's any font you want to use
pdfMake.fonts = {
  Roboto: {
    normal: window.location.origin + "/fonts/Inter-Regular.ttf",
    bold: window.location.origin + "/fonts/Inter-Bold.ttf",
  },
};
```
...

Create helper function to build document object
```javascript
// to get label of section, there will be 3 section: Experience, Skill and Interest
function getSectionLabel(text) {
  return { text, style: ["textBlue", "bold"], margin: [0, 0, 0, 5] };
}

// our sections and their values will be wrapped into tables, so we need the function below to simplify creating the tables
function generateTable(body) {
  return {
    table: {
      widths: [150, "*"],
      body,
    },
    layout: "noBorders",
  };
}
```

Let’s map our data and generate the table with generateTable() function
```javascript
// generate experiences
const generatedExperiences = experiences.map((experience) => {
  return [
    experience.date,
    {
      stack: [
        { text: experience.position, style: ["bold"] },
        { text: experience.company, margin: [0, 0, 0, 5] },
        {
          ul: experience.jobs,
        },
        "\n",
      ],
    },
  ];
});
const generatedExperienceTable = generateTable(generatedExperiences);

// generate skills
const generatedSkills = skills
  .map((skill) => {
    return ["", { ul: [skill.label] }];
  });
const generatedSkillTable = generateTable(generatedSkills);

// generate interests
const generatedInterests = interests.map((interest) => {
  return ["", { ul: [interest] }];
});
const generatedInterestTable = generateTable(generatedInterests);
```

Then we create the document object
```javascript
var dd = {
  content: [
    {
      text: "John Doe", 
      style: "header"
    },
    "\n",
    {
      text: "t.me/johndoe007 | johndoe@coolmail.com",
      margin: [0, 0, 0, 3],
    },
    "\n",
    getSectionLabel("WORK EXPERIENCE"),
    generatedExperienceTable,
    "\n",
    getSectionLabel("SKILL"),
    generatedSkillTable,
    "\n",
    getSectionLabel("INTEREST"),
    generatedInterestTable,
  ],
  styles: {
    header: {
      fontSize: 18,
      bold: true,
    },
    small: {
      fontSize: 10,
    },
    bold: {
      bold: true,
    },
    textBlue: {
      color: "#3576ba",
    },
  },
  defaultStyle: {
    fontSize: 10,
    font: "Roboto",
  },
};
```

The last but not least, create the PDF file and download it. You can just open the file too with .open() function.
```javascript
pdfMake.createPdf(dd).download("Awesome CV");
```

The full code is here:
```javascript
import pdfMake from "pdfmake/build/pdfmake";

const experiences = [
  {
    position: "Back End Web Developer",
    company: "ABCD Company",
    date: "Dec 2021 – Current",
    jobs: ["Do something", "Do something else", "Doing it again"]
  },
  {
    position: "Front End Web Developer",
    company: "EFG Company",
    date: "Jan 2021 – Dec 2021",
    jobs: ["Do something", "Do something else", "Doing it again"]
  }
];

const skills = [
  "Javascript",
  "NodeJS",
  "React.js",
  "Vue.js",
  "PostgreSQL",
  "MongoDB"
];

const interests = ["Programming", "Web Design"];

// if there's any font you want to use
pdfMake.fonts = {
  Roboto: {
    normal: window.location.origin + "/fonts/Inter-Regular.ttf",
    bold: window.location.origin + "/fonts/Inter-Bold.ttf",
  },
};

// to get label of section, there will be 3 section: Experience, Skill and Interest
function getSectionLabel(text) {
  return { text, style: ["textBlue", "bold"], margin: [0, 0, 0, 5] };
}

// our sections and their values will be wrapped into tables, so we need the function below to simplify creating the tables
function generateTable(body) {
  return {
    table: {
      widths: [150, "*"],
      body,
    },
    layout: "noBorders",
  };
}

// generate experiences
const generatedExperiences = experiences.map((experience) => {
  return [
    experience.date,
    {
      stack: [
        { text: experience.position, style: ["bold"] },
        { text: experience.company, margin: [0, 0, 0, 5] },
        {
          ul: experience.jobs,
        },
        "\n",
      ],
    },
  ];
});
const generatedExperienceTable = generateTable(generatedExperiences);

// generate skills
const generatedSkills = skills
  .map((skill) => {
    return ["", { ul: [skill] }];
  });
const generatedSkillTable = generateTable(generatedSkills);

// generate interests
const generatedInterests = interests.map((interest) => {
  return ["", { ul: [interest] }];
});
const generatedInterestTable = generateTable(generatedInterests);

var dd = {
  content: [
    {
      text: "John Doe",
      style: "header",
    },
    "\n",
    {
      text: "t.me/johndoe007 | johndoe@coolmail.com",
      margin: [0, 0, 0, 3],
    },
    "\n",
    getSectionLabel("WORK EXPERIENCE"),
    generatedExperienceTable,
    "\n",
    getSectionLabel("SKILL"),
    generatedSkillTable,
    "\n",
    getSectionLabel("INTEREST"),
    generatedInterestTable,
  ],
  styles: {
    header: {
      fontSize: 18,
      bold: true,
    },
    small: {
      fontSize: 10,
    },
    bold: {
      bold: true,
    },
    textBlue: {
      color: "#3576ba",
    },
  },
  defaultStyle: {
    fontSize: 10,
    font: "Roboto",
  },
};

pdfMake.createPdf(dd).download("Awesome CV");
```

The result will look like this:
![result](/blog/generate-pdf-with-pdfmake/image.png)

You can do more complex structures of pdf document if needed, you can explore the documentation of the package [here](https://pdfmake.github.io/docs/0.1/).