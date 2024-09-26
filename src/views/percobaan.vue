<script setup lang="ts">
import { ref, shallowRef } from 'vue';

import BaseBreadcrumb from '@/components/shared/BaseBreadcrumb.vue';
import UiParentCard from '@/components/shared/UiParentCard.vue';

const page = ref({ title: 'Percobaan' });
const breadcrumbs = shallowRef([
  {
    title: 'Others',
    disabled: false,
    href: '#'
  },
  {
    title: 'Sample Page',
    disabled: true,
    href: '#'
  }
]);

     const books = ref([]); // Populate this with the list of books from your data
     const chapters= ref([]); // Populate this with chapters based on the selected book
     const verses= shallowRef([
       { id: 1, originalText: 'asd', annotations: 'asd'  },
       { id: 2, originalText: 'asd2', annotations: 'asd2'  }
     ]); // This will hold the verses for the selected chapter
     const translations= shallowRef([
        { id: 'asd', verseId: 1, text: 'asd', version: 'asd', translator: 'asd' },
         ]);
     var annotations:string;
     var selectedVersion: string;
     const selectedBook= ref(null);
     const selectedChapter= ref(null);

    function fetchChapters() {
      // Fetch chapters based on selected book
      // Example: this.chapters = fetchChaptersFromAPI(this.selectedBook);
    }
    function fetchVerses() {
      // Fetch verses based on selected chapter
      // Example: this.verses = fetchVersesFromAPI(this.selectedBook, this.selectedChapter);
    }
    function updateAnnotation(verse: any) {
      // Update the annotation for the verse
      // Example: saveAnnotationToAPI(verse.number, verse.annotation);
    }
    function toggleAnnotations(verse: any){
      
    }
function editTranslation(id: string){}
function addNewTranslation(id: number){}
    

</script>

<template>
  <BaseBreadcrumb :title="page.title" :breadcrumbs="breadcrumbs"></BaseBreadcrumb>
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
                            :items="translation.version"
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
</template>

