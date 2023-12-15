<template>
  <div id="app" class="bg-gray-100 min-h-screen flex justify-center items-center p-8">
    <quiz-board :categories="categoriesWithAnsweredInfo" :difficulties="difficulties" @cell-clicked="handleCellClicked" />
    <question-modal :show="showModal" :question="currentQuestion" :answer="currentAnswer" @close="handleModalClose" />
  </div>
</template>
  
<script>
import QuizBoard from './components/QuizBoard.vue';
import QuestionModal from './components/QuestionModal.vue';

export default {
  name: 'App',
  components: {
    QuizBoard,
    QuestionModal
  },
  data() {
    return {
      categories: [
        {
          id: 1,
          name: 'Hip-Hop',
          questions: {
            100: { question: 'Gesucht ( Buzzer ): Rapper Duo', answer: 'Kollegah & Farid Bang' },
            200: { question: 'Wie viele monatlich Spotify Höhrer*innen hat Nicky Minaj?', answer: '52.015.068' },
            300: { question: 'Welcher Artist heißt mit bürgerlichen Namen < Name > ?', answer: 'Mac Miller' },
            400: { question: 'Wie heißt und wo findet eines der größten Hip Hop Festivals in einem Nachbarland von Deutschland statt?', answer: 'Frauenfeld Festival in der Schweiz' },
            500: { question: 'Gesucht ( Buzzer ): Titel, Künstler*in und Heimatstadt mit Viertel', answer: 'Breaking your Heart - Apache 207 - Ludwigshafen Gartenstadt' }
          }
        },
        {
          id: 2,
          name: 'Indie',
          questions: {
            100: { question: 'Gesucht ( Buzzer ): Band und Songtitel', answer: 'Kings of Leon - Use Somebody' },
            200: { question: 'Gesucht ( Buzzer ): Band und Songtitel', answer: 'Milky Chance - Stolen Dance' },
            300: { question: 'Gesucht ( Buzzer ): Lied und Artist', answer: 'Oasis - Don´t Look Back In Anger' },
            400: { question: 'Wie hieße die Band, die Vielleicht, Vielleicht mit Pocahontas 3 Tage ans Meer fahren will, wenn sie die Vor- anstatt der Nachnamen genommen hätten?', answer: 'ChristopherHenningSeverin' },
            500: { question: 'Gesucht ( Buzzer ): Artist und Album', answer: 'Noah Kahan - Stick Season' }
          }
        },
        {
          id: 3,
          name: 'Filmmusik',
          questions: {
            100: { question: 'Aus welchem Filmt stammt folgender Soundtrack?', answer: 'Der Pate' },
            200: { question: 'Gesucht ( Buzzer ): Film', answer: 'Frozen - Die Eiskönigin' },
            300: { question: 'Gesucht ( Buzzer ): Komponist', answer: 'John Williams' },
            400: { question: 'Wie oft war Hans Zimmer für den Oscar nominiert', answer: '12 ( 2 gewonnen )' },
            500: { question: 'Aus welchen Serien stammen folgende Intros?', answer: 'Prince of bell air, Friends, Game of Thrones, Die Simpsons, Big Bang Theory, Modern Family, The Office, How I Met Your Mother, Breaking Bad, Pokémon, Scrubs, Family Guy' }
          }
        },
        {
          id: 4,
          name: 'Klassiker',
          questions: {
            100: { question: 'Gesucht ( Buzzer ): Band', answer: 'AC/DC' },
            200: { question: 'Gesucht ( Buzzer ): Original Song', answer: 'Girls just wanna have fun' },
            300: { question: 'Gesucht ( Buzzer ): Band', answer: 'Queen' },
            400: { question: 'Gesucht ( Buzzer ): Song', answer: 'Micheal Jackson - Thriller' },
            500: { question: 'Mit Now and Then erschien vor kurzem ein neues Lied einer Band, die es eigentlich schon sehr lange nicht gibt. Nennt zwei Mitglieder der Band mit zugehörigem Hauptinstrument', answer: 'The Beatles' }
          }
        },
        {
          id: 5,
          name: 'Rock',
          questions: {
            100: { question: 'Wann fand das legendäre Woodstockfestival statt?', answer: '1969' },
            200: { question: 'Gesucht ( Buzzer ): Interpret und Songtitel', answer: 'RHCP - Californication' },
            300: { question: 'Wie viele Wochen waren Dark Side of the Moon von Pink Floyd ununterbrochen in den Billboard Top 200?', answer: '917 - 17,5 Jahre' },
            400: { question: 'Aus welchem Lied stammen folgende Zeilen?', answer: 'Linkin Park - In the End' },
            500: { question: 'Gesucht ( Buzzer ): Person', answer: 'Jimi Hendrix' }
          }
        },
        {
          id: 6,
          name: 'Pop',
          questions: {
            100: { question: 'Wer singt diese Lieder?', answer: 'Justin Bieber' },
            200: { question: 'Schreibt so viele Taylor Swift Alben auf wie ihr kennt.', answer: '...' },
            300: { question: 'Mit wem produzierte Bizarrap diesen Song und gegen wen ist er gerichtet?', answer: 'Shakira, Pique' },
            400: { question: 'Welcher Künstler ist gesucht?', answer: 'Alexander Marcus' },
            500: { question: 'Nenne in 2 Minuten so viele Globale Top 10 Spotify Artists 2023, pro Richtige Nennung 50 Punkte', answer: '...' }
          }
        }
      ],
      difficulties: [100, 200, 300, 400, 500],
      answeredQuestions: new Set(), // To track answered questions
      showModal: false,
      currentQuestion: ''
    };
  },
  computed: {
    categoriesWithAnsweredInfo() {
      return this.categories.map(category => ({
        ...category,
        questions: Object.fromEntries(
          Object.entries(category.questions).map(([difficulty, question]) => [
            difficulty,
            { ...question, isAnswered: this.answeredQuestions.has(`${category.id}-${difficulty}`) }
          ])
        )
      }));
    }
  },
  methods: {
    handleCellClicked(category, difficulty) {
      const questionInfo = category.questions[difficulty];
      if (!this.answeredQuestions.has(`${category.id}-${difficulty}`)) {
        this.currentQuestion = questionInfo.question;
        this.currentAnswer = questionInfo.answer; // Add this line
        this.showModal = true;
        this.answeredQuestions.add(`${category.id}-${difficulty}`);
      }
    },
    handleModalClose() {
      this.showModal = false;
    },
    isQuestionAnswered(categoryId, difficulty) {
      return this.answeredQuestions.some(q => q.category === categoryId && q.difficulty === difficulty);
    }
  }

};
</script>
  
<style>
/* Add any global styles you want here */
</style>
  