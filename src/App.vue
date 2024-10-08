<script>
import ResumeSection from './components/ResumeSection.vue'
import SectionHeadline from './components/SectionHeadline.vue'
import ContactForm from './components/ContactForm.vue'

export default {
  components: {
    ResumeSection,
    SectionHeadline,
    ContactForm
  },
  data() {
    return {
      name: 'Suresh Koochana',
      title: 'Software Engineer II',
      introText: 'Building web apps from scratch, I am passionate about web technologies.',
      imageUrl: './minion.jpg',
      headlines: ['About me', 'Contact', 'Skills', 'Certifications', 'Experience', 'Education'],
      contact: {
        phone: '15713909584',
        email: 'kuchana123.suresh@gmail.com',
        address: 'Main St 100, 19777 NY'
      },
      skills: [
        'ReactJS',
        'VueJS',
        'NextJS',
        'HTML/CSS',
        'RestFul API/ GraphQL',
        'Docker',
        'PostgreSQL'
      ],
      experience: [
        {
          title: 'Senior Data Scientist',
          company: 'ABC Analytics Inc.',
          location: 'London',
          date: '2022 - Present',
          description: [
            'Led a team of data scientists in developing advanced machine learning models for predictive analytics',
            'Designed and implemented a recommendation system that boosted cross-selling, leading to a 20% increase in revenue',
            'Conducted A/B testing and statistical analysis to optimize product features'
          ]
        },
        {
          title: 'Data Scientist',
          company: 'XYZ Data Solutions',
          location: 'London',
          date: '2017 - 2019',
          description: [
            'Developed and deployed machine learning models for fraud detection, reducing fraudulent transactions by 18%',
            'Conducted in-depth exploratory data analysis to identify key trends and insights',
            'Worked on data preprocessing, feature engineering, and model selection to improve model performance'
          ]
        },
        {
          title: 'Data Scientist Trainee',
          company: 'Data Insights Ltd.',
          location: 'New York City',
          date: '2016-2017',
          description: [
            "Collaborated with external partners to integrate third-party data sources, expanding the company's data assets and enhancing predictive modeling capabilities.",
            'Presented data-driven insights and recommendations to executive leadership, influencing strategic decisions and driving revenue growth.'
          ]
        }
      ],
      education: [
        {
          title: 'Master of Science in Data Science',
          university: 'StellarTech University',
          location: 'Starville',
          date: '2020-2022',
          description: [
            'Coursework included advanced machine learning, statistical modeling, and data visualization techniques.',
            "Thesis: 'Predictive Modeling for Customer Churn in E-commerce using Random Forest.'"
          ]
        },
        {
          title: 'Bachelor of Science in Computer Science',
          university: 'Evergreen State University',
          location: 'Springdale',
          date: '2012-2015',
          description: [
            'Relevant coursework in database management, algorithms, and programming languages.',
            "Senior project: 'Development of a Recommender System for Movie Ratings.'"
          ]
        }
      ],
      highlights: [
        'React Native by Meta(Coursera)',
        'React handle large scale applications (Linkedin)'
      ]
    }
  },
  methods: {
    updateHeadline(newValue, index) {
      this.headlines[index] = newValue
    },
    updateProperty(event, key) {
      this[key] = event.target.innerText
    },
    updateNestedProperty(event, key1, key2) {
      this[key1][key2] = event.target.innerText
    },
    updateExperience(event, key, index) {
      this.experience[index][key] = event.target.innerText
    },
    updateExperienceDescription(event, index, key) {
      this.experience[index].description[key] = event.target.innerText
    },
    updateEducation(event, key, index) {
      this.education[index][key] = event.target.innerText
    },
    updateEducationDescription(event, index, key) {
      this.education[index].description[key] = event.target.innerText
    }
  }
}
</script>

<template>
  <main class="container">
    <div id="resume" class="d-flex">
      <div class="left-col">
        <ResumeSection>
          <img :src="imageUrl" alt="minion" class="profile-pic" />

          <SectionHeadline :headline="headlines[0]" @headline-edited="updateHeadline($event, 0)" />

          <div contenteditable="true" @input="updateProperty($event, 'introText')">
            {{ introText }}
          </div>
        </ResumeSection>

        <ResumeSection>
          <SectionHeadline :headline="headlines[1]" @headline-edited="updateHeadline($event, 1)" />
          <ContactForm :contact="contact" @edit-contact="updateNestedProperty" />
        </ResumeSection>

        <ResumeSection>
          <SectionHeadline :headline="headlines[2]" @headline-edited="updateHeadline($event, 2)" />
          <ul>
            <li
              v-for="(skill, index) in skills"
              :key="index"
              contenteditable="true"
              @input="updateNestedProperty($event, 'skills', index)"
            >
              {{ skill }}
            </li>
          </ul>
        </ResumeSection>

        <ResumeSection>
          <SectionHeadline :headline="headlines[3]" @headline-edited="updateHeadline($event, 3)" />

          <ul>
            <li
              v-for="(highlight, index) in highlights"
              :key="index"
              contenteditable="true"
              @input="updateNestedProperty($event, 'highlights', index)"
            >
              {{ highlight }}
            </li>
          </ul>
        </ResumeSection>
      </div>
      <div class="right-col">
        <div class="personal-name" contenteditable="true" @input="updateProperty($event, 'name')">
          {{ name }}
        </div>
        <div class="personal-title" contenteditable="true" @input="updateProperty($event, 'title')">
          {{ title }}
        </div>
        <ResumeSection>
          <h4 class="section-headline" contenteditable="true" @input="updateHeadline($event, 4)">
            {{ headlines[4] }}
          </h4>

          <div v-for="(item, index) in experience" :key="index" class="inner-section">
            <div contenteditable="true" @input="updateExperience($event, 'title', index)">
              {{ item.title }}
            </div>
            <div class="d-flex justify-content-between">
              <div>
                <span contenteditable="true" @input="updateExperience($event, 'company', index)">{{
                  item.company
                }}</span
                >,
                <span contenteditable="true" @input="updateExperience($event, 'location', index)">{{
                  item.location
                }}</span>
              </div>
              <div contenteditable="true" @input="updateExperience($event, 'date', index)">
                {{ item.date }}
              </div>
            </div>
            <ul>
              <li
                v-for="(desc, innerIndex) in item.description"
                :key="innerIndex"
                contenteditable="true"
                @input="updateExperienceDescription($event, index, innerIndex)"
              >
                {{ desc }}
              </li>
            </ul>
          </div>
        </ResumeSection>
        <ResumeSection>
          <SectionHeadline :headline="headlines[5]" @headline-edited="updateHeadline($event, 5)" />

          <div v-for="(item, index) in education" :key="index">
            <div contenteditable="true" @input="updateEducation($event, 'title', index)">
              {{ item.title }}
            </div>
            <div class="d-flex justify-content-between">
              <div>
                <span @input="updateEducation($event, 'university', index)">{{
                  item.university
                }}</span
                >,<span @input="updateEducation($event, 'location', index)">{{
                  item.location
                }}</span>
              </div>
              <div @input="updateEducation($event, 'date', index)">{{ item.date }}</div>
            </div>
            <ul>
              <li
                v-for="(desc, innerIndex) in item.description"
                :key="innerIndex"
                @input="updateEducationDescription($event, index, innerIndex)"
              >
                {{ desc }}
              </li>
            </ul>
          </div>
        </ResumeSection>
      </div>
    </div>
  </main>
</template>

<style scoped>
#resume {
  box-shadow:
    rgba(50, 50, 93, 0.25) 0px 13px 27px -5px,
    rgba(0, 0, 0, 0.3) 0px 8px 16px -8px;
  height: 297mm;
  width: 210mm;
}

.left-col {
  background-color: var(--background-color-left);
  color: var(--text-color-left);
  border-right: 1px solid var(--highlight-color-left);
  width: 30%;
  padding: 30px;
}

.right-col {
  background-color: var(--background-color-right);
  color: var(--text-color-right);
  width: 70%;
  padding: 30px;
}

.personal-name {
  font-weight: 300;
  color: var(--highlight-color-right);
  font-size: 28px;
  border-bottom: 1px solid var(--highlight-color-right);
  margin: 0;
  margin-left: -30px;
  padding-left: 30px;
  padding-bottom: 15px;
}

.personal-title {
  border-bottom: 1px solid var(--highlight-color-right);
  margin: 0 0 20px -30px;
  padding: 15px 0 15px 30px;
  font-weight: 300;
  font-size: 20px;
}

#resume ul {
  padding-inline-start: 16px;
  margin-block-end: 0px;
  margin-block-start: 5px;
}

.profile-pic {
  display: block;
  width: 160px;
  height: 160px;
  border: 5px solid var(--highlight-color-left);
  margin-bottom: 20px;
  object-fit: cover;
  margin-left: auto;
  margin-right: auto;
  border-radius: 50%;
}

.inner-section {
  margin-bottom: 20px;
}
</style>
