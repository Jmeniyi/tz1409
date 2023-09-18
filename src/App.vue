<template>
  <div id="App">
    <div id="buttonsComponent">
      <div class="container">
        <button @click="undo" :disabled="historyIndex <= 0">
          <img src="./assets/img/Group1.svg" alt="Button Back">
        </button>
        <button @click="redo">
          <img src="./assets/img/Group2.svg" alt="Button UP">
        </button>
        <button @click="convertToUpperCase">
          <img src="./assets/img/Group5.svg" alt="Button convert to UpperCase">
        </button>
        <button @click="convertToLowerCase">
          <img src="./assets/img/Group3.svg" alt="Button convertToLowerCase">
        </button>
        <button @click="uploadImage">
          <img class="container__img" src="./assets/img/Group4.svg" alt="Button upload IMG">
        </button>
        <button @click="copyHTML">
          <a class="buttonsComponent__container_button_copyHTML">Скопировать HTML</a>
        </button>
      </div>
    </div>
    <div class="mainText">
      <div class="mainText__textArea" contenteditable="true" @input="updateContent" v-html="text"></div>
      <h1 class="mainText__textHead">{{ textHead }}</h1>
      <img class="mainText__mainImg" src="./assets/img/image1.png" alt="Monkey">
      <p class="mainText__text2">{{ text2 }}</p>
    </div>
  </div>
</template>

<script>
import { defineComponent } from 'vue';
export default defineComponent({
  name: 'App',
  components: {
  },
  data() {
    return {
      text: 'Таким образом консультация с широким активом представляет собой интересный эксперимент проверки позиций, занимаемых участниками в отношении поставленных задач. С другой стороны постоянное информационно-пропагандистское обеспечение нашей деятельности представляет собой интересный эксперимент проверки форм развития. Идейные соображения высшего порядка, а также укрепление и развитие структуры влечет за собой процесс внедрения и модернизации соответствующий условий активизации. Задача организации, в особенности же реализация намеченных плановых заданий играет важную роль в формировании дальнейших направлений развития. Повседневная практика показывает, что постоянное информационно-пропагандистское обеспечение нашей деятельности играет важную роль в формировании существенных финансовых и административных условий.',
      textHead: 'Смотрите какие обезьянки',
      text2: 'Таким образом консультация с широким активом представляет собой интересный эксперимент проверки позиций, занимаемых участниками в отношении поставленных задач. С другой стороны постоянное информационно-пропагандистское обеспечение нашей деятельности представляет собой инйцу шо шщйоц ущойц ущошцщйуо йцщуо йщцоу щйоу шщйцош ущйтересный эксперимент проверки форм развития. Идейные соображения высшего порядка, а также укрепление и развитие структуры влечет за собой процесс внедрения и модернизации соответствующий условий активизации. Задача организации, в особенности же реализация намеченных плановых заданий играет важную роль в формировании дальнейших направлений развития. Повседневная практика показывает, что постоянное информационно-пропагандистское обеспечение нашей деятельности играет важную роль в формировании существенных финансовых и административных условий.\n Товарищи! новая модель организационной деятельности требуют от нас анализа направлений прогрессивного развития. Задача организации, в особенности же постоянный количественный рост и сфера нашей активности требуют от нас анализа позиций, занимаемых участниками в отношении поставленных задач. Задача организации, в особенности же реализация намеченных плановых заданий требуют от нас анализа системы обучения кадров, соответствует насущным потребностям.',
      history: ['Таким образом консультация с широким активом представляет собой интересный эксперимент проверки позиций, занимаемых участниками в отношении поставленных задач. С другой стороны постоянное информационно-пропагандистское обеспечение нашей деятельности представляет собой интересный эксперимент проверки форм развития. Идейные соображения высшего порядка, а также укрепление и развитие структуры влечет за собой процесс внедрения и модернизации соответствующий условий активизации. Задача организации, в особенности же реализация намеченных плановых заданий играет важную роль в формировании дальнейших направлений развития. Повседневная практика показывает, что постоянное информационно-пропагандистское обеспечение нашей деятельности играет важную роль в формировании существенных финансовых и административных условий.',
      ],
      historyIndex: 0,
    }
  },
  methods: {
    updateContent(event) {
      this.history = this.history.slice(0, this.historyIndex + 1);
      this.history.push(event.target.innerHTML);
      this.historyIndex++;
      this.text = event.target.innerHTML;
    },
    undo() {
      if (this.historyIndex >= 0) {
        this.historyIndex--;
        this.text = this.history[this.historyIndex];
      }
    },
    redo() {
      if (this.historyIndex < this.history.length - 1) {
        this.historyIndex++;
        this.text = this.history[this.historyIndex];
      }
    },
    convertToUpperCase() {
      const selection = window.getSelection().toString();
      const upperCaseSelection = selection.toUpperCase();
      const updatedText = this.text.replace(selection, upperCaseSelection);
      this.text = updatedText;
    },
    convertToLowerCase() {
      const selection = window.getSelection().toString();
      const upperCaseSelection = selection.toLowerCase();
      const updatedText = this.text.replace(selection, upperCaseSelection);
      this.text = updatedText;
    },
    handleFileUpload(event) {
      const file = event.target.files[0];
    },
    uploadImage() {
      const formData = new FormData();
      const fileInput = document.createElement('input');
      fileInput.type = 'file';
      fileInput.accept = 'image/*';
      fileInput.onchange = (event) => {
        const file = event.target.files[0];
        formData.append('image', file);
        const imageURL = 'anyURLAdress';

        const imgHTML = `<img src="${imageURL}" alt="Uploaded image">`;
        this.text += imgHTML;
      };
      fileInput.click();
    },
    copyHTML() {
      const htmlToCopy = document.documentElement.outerHTML;

      const tempInput = document.createElement('input');
      tempInput.setAttribute('value', htmlToCopy);
      document.body.appendChild(tempInput);
      tempInput.select();
      document.execCommand('copy');
      document.body.removeChild(tempInput);


      alert('HTML скопирован в буфер обмена!');
    }
  },
});
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background: #1E1E1E;
  width: 100%;
  height: 100%;
}

#App {
  padding-left: 107px;
}

#buttonsComponent {
  margin-top: 77px;
  margin-bottom: 31px;
  width: min-content;
  height: min-content;
}

.container {
  display: flex;
  gap: 12px;
  width: min-content;
  height: min-content;
  text-align: center;
  justify-content: center;
  align-items: center;
}

.container__button {
  border: none;
}

.container__img {
  height: 42px;
  width: 38px;
}

.buttonsComponent__container_button_copyHTML {
  color: #639EFF;
  font-family: Roboto;
  font-size: 15px;
  font-style: normal;
  font-weight: 400;
  line-height: 23px;
  /* 153.333% */
  position: relative;
  text-align: center;
  white-space: nowrap;
}

.mainText__textArea {
  width: 621px;
  color: #EAEAEA;
  font-family: Roboto;
  font-size: 15px;
  font-style: normal;
  font-weight: 400;
  line-height: 23px;
  /* 153.333% */
  overflow: hidden;
  resize: none;
  height: auto;
  border: none;
}

.mainText__textHead {
  color: #FFF;
  font-family: Roboto;
  font-size: 31px;
  font-style: normal;
  font-weight: 400;
  line-height: 23px;
  /* 74.194% */
  margin-top: 46px;
  margin-bottom: 33px;
  height: min-content;
  width: 621px;
}

.mainText__mainImg {
  width: 739px;
  height: 308px;
  border-radius: 4px;
  background: url(./assets/img/image1.png), lightgray 50% / cover no-repeat;
  margin-bottom: 31px;
}

.mainText__text2 {
  height: auto;
  width: 621px;
  color: #EAEAEA;
  font-family: Roboto;
  font-size: 15px;
  font-style: normal;
  font-weight: 400;
  line-height: 23px;
  /* 153.333% */
  border: none;
  padding-bottom: 107px;
  white-space: pre-line
}
</style>