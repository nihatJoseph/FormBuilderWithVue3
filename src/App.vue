<template>
  <div id="app" class="container-sm"></div>
  <div class="row">
    <div class="col-sm-12">
      <div class="row flex-fill">
        <div class="col-sm-4 mx-auto my-4">
          <div class="card d-flex align-items-center">
            <p class="mx-1 my-2"><strong>Select Tag</strong></p>
            <div class="form-check mx-1 my-2">
              <input
                v-model="tagSelected"
                value="textBox"
                class="form-check-input"
                type="radio"
                name="SelectTag"
                id="flexRadioDefault1"
              />
              <label class="form-check-label" for="flexRadioDefault1">
                Text Box
              </label>
            </div>
            <div class="form-check mx-1 my-2">
              <input
                v-model="tagSelected"
                value="textArea"
                class="form-check-input"
                type="radio"
                name="SelectTag"
                id="flexRadioDefault1"
              />
              <label class="form-check-label" for="flexRadioDefault1">
                Text Area
              </label>
            </div>
            <div class="form-check mx-1 my-2">
              <input
                v-model="tagSelected"
                value="checkBox"
                class="form-check-input"
                type="radio"
                name="SelectTag"
                id="flexRadioDefault1"
              />
              <label class="form-check-label" for="flexRadioDefault1">
                Checkbox
              </label>
            </div>
            <div class="form-check mx-1 my-2">
              <input
                v-model="tagSelected"
                value="button"
                class="form-check-input"
                type="radio"
                name="SelectTag"
                id="flexRadioDefault1"
              />
              <label class="form-check-label" for="flexRadioDefault1">
                Button
              </label>
            </div>
          </div>
        </div>
        <div class="col-sm-4 mx-auto my-4">
          <div class="card d-flex align-items-center">
            <p class="mx-1 my-2">
              <strong>Select Info</strong>
            </p>
            <input
              v-model="title"
              type="text"
              class="form-control"
              placeholder="Title"
              aria-label="Title"
            />
            <input
              v-model="placeHolder"
              v-if="tagSelected == 'textBox' || tagSelected == 'textArea'"
              type="text"
              class="form-control"
              placeholder="Placeholder"
              aria-label="Title"
            />
            <select v-model="language" class="form-select">
              <option disabled value="">Language</option>
              <option value="Turkish">Turkish</option>
              <option value="English">English</option>
              <option value="Arabic">Arabic</option>
            </select>
          </div>
        </div>
        <div class="col-sm-4 mx-auto my-4">
          <div class="card d-flex align-items-center">
            <p class="mx-1 my-2"><strong>Select Validation</strong></p>
            <div class="form-check mx-1 my-2">
              <input
                v-model="validation.required"
                :value="true"
                class="form-check-input"
                type="radio"
                name="Validation1"
                id="flexRadioDefault1"
              />
              <label class="form-check-label" for="flexRadioDefault1">
                Required
              </label>
            </div>
            <div class="form-check mx-1 my-2">
              <input
                v-model="validation.number"
                :value="true"
                class="form-check-input"
                type="radio"
                name="Validation"
                id="flexRadioDefault1"
              />
              <label class="form-check-label" for="flexRadioDefault1">
                Number
              </label>
            </div>
            <div class="form-check mx-1 my-2">
              <input
                v-model="validation.email"
                :value="true"
                class="form-check-input"
                type="radio"
                name="Validation"
                id="flexRadioDefault1"
              />
              <label class="form-check-label" for="flexRadioDefault1">
                E-mail
              </label>
            </div>
          </div>
        </div>
      </div>
      <div class="d-flex justify-content-center">
        <button @click="saveElement" type="button" class="btn btn-success">
          Kaydet
        </button>
      </div>
      <div class="card mx-3 my-3">
        <p class="card-header mx-3 my-3">{{ elementLenght }}</p>
        <p
          class="card-body mx-3 my-3"
          v-for="(value, index) in myElements"
          :key="index"
        >
          Id: {{ index + 1 }} <br />
          Tag: {{ value.tagSelected }} <br />
          Title: {{ value.title }} <br />
          Placeholder: {{ value.placeHolder }} <br />
          Language: {{ value.language }} <br />
          Validations: {{ value.validation.required ? "Required" : "" }}
          {{ value.validation.number ? "Number" : "" }}
          {{ value.validation.email ? "Email" : "" }} <br />
          <button @click="deleteElement(index)" class="btn btn-danger">
            Sil
          </button>
        </p>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      myElements: [],
      tagSelected: null,
      title: null,
      placeHolder: null,
      validation: {
        required: false,
        number: false,
        email: false,
      },
      language: "",
    };
  },
  methods: {
    saveElement() {
      if (this.tagSelected && this.title) {
        this.myElements.push({
          tagSelected: this.tagSelected,
          title: this.title,
          placeHolder: this.placeHolder,
          validation: this.validation,
          language: this.language,
        });
        this.formClear();
      } else {
        window.alert("lütfen forma bilgilerinizi giriniz.");
      }

      console.log(this.myElements);
    },
    formClear() {
      this.tagSelected = null;
      this.title = null;
      this.placeHolder = null;
      this.validation = {
        required: false,
        number: false,
        email: false,
      };
      this.language = "";
    },
    deleteElement(index) {
      this.myElements.splice(index, 1);
    },
  },
  computed: {
    elementLenght() {
      return "Toplam element sayısı: " + this.myElements.length;
    },
  },
};
</script>
