      <v-container fluid>
        <v-row>
          <v-col cols="12">
            <v-select
              v-model="selectedBook"
              :items="books"
              label="Select Book"
              @change="fetchChapters"
            ></v-select>
            <v-select
              v-model="selectedChapter"
              :items="chapters"
              label="Select Chapter"
              @change="fetchVerses"
            ></v-select>
          </v-col>
        </v-row>

        <v-row>
          <v-col cols="6">
            <v-card>
              <v-card-title>Original Text</v-card-title>
              <v-card-text>
                <v-list>
                  <v-list-item-group>
                    <v-list-item v-for="verse in verses" :key="verse.id">
                      <v-list-item-content>
                        <v-list-item-title>{{ verse.originalText }}</v-list-item-title>
                        <v-list-item-subtitle>
                          <v-btn small @click="toggleAnnotations(verse.id)">Annotations</v-btn>
                          <v-expand-transition>
                            <div v-if="annotations[verse.id]">
                              <p>{{ verse.annotations }}</p>
                            </div>
                          </v-expand-transition>
                        </v-list-item-subtitle>
                      </v-list-item-content>
                    </v-list-item>
                  </v-list-item-group>
                </v-list>
              </v-card-text>
            </v-card>
          </v-col>

          <v-col cols="6">
            <v-card>
              <v-card-title>Translations</v-card-title>
              <v-card-text>
                <v-list>
                  <v-list-item-group>
                    <v-list-item v-for="translation in translations" :key="translation.id">
                      <v-list-item-content>
                        <v-list-item-title>
                          {{ translation.text }} (v{{ translation.version }} by {{ translation.translator }})
                        </v-list-item-title>
                        <v-list-item-subtitle>
                          <v-select
                            v-model="selectedVersion[translation.verseId]"
                            :items="translation.versions"
                            label="Select Version"
                          ></v-select>
                          <v-btn small @click="editTranslation(translation.id)">Edit</v-btn>
                          <v-btn small @click="addNewTranslation(translation.verseId)">Add New</v-btn>
                        </v-list-item-subtitle>
                      </v-list-item-content>
                    </v-list-item>
                  </v-list-item-group>
                </v-list>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-container>

  <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/vuetify@2.6.12/dist/vuetify.js"></script>
  <script>
    new Vue({
      el: '#app',
      vuetify: new Vuetify(),
      data: {
        books: ['Genesis', 'Exodus', 'Leviticus'], // Add more books
        selectedBook: null,
        chapters: [], // Will populate based on selected book
        selectedChapter: null,
        verses: [], // Will populate based on selected chapter
        translations: [], // Will populate with translations for the selected chapter
        annotations: {},
        selectedVersion: {}
      },
      methods: {
        fetchChapters() {
          // Fetch chapters based on selectedBook
          // For now, use hardcoded chapters as an example
          this.chapters = ['1', '2', '3']; // Update with actual chapter fetching
        },
        fetchVerses() {
          // Fetch verses based on selectedChapter
          // For now, use hardcoded verses as an example
          this.verses = [
            { id: 1, originalText: 'In the beginning...', annotations: 'Note about this verse.' },
            { id: 2, originalText: 'And the earth was without form...', annotations: 'Another note.' }
          ];
          this.translations = [
            { id: 1, verseId: 1, text: 'In the beginning, God created...', version: 1, translator: 'John Doe', versions: [1, 2] },
            { id: 2, verseId: 2, text: 'And the earth was formless...', version: 1, translator: 'Jane Smith', versions: [1] }
          ];
        },
        toggleAnnotations(verseId) {
          // Toggle annotation visibility
          this.$set(this.annotations, verseId, !this.annotations[verseId]);
        },
        editTranslation(id) {
          // Edit translation logic here
          alert(`Editing translation ${id}`);
        },
        addNewTranslation(verseId) {
          // Logic to add a new translation for the verse
          alert(`Adding new translation for verse ${verseId}`);
        }
      }
    });
  </script>
