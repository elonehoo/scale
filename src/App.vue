<script setup lang="ts">
import { ref } from 'vue'
import Footer from '~/components/Footer.vue'
import BackgroundSelector from '~/components/BackgroundSelector.vue'
import MainColorSelector from '~/components/MainColorSelector.vue'
import DynamicInput from './components/DynamicInput.vue'
import ColorsRow from './components/ColorsRow.vue'
import Triggers from './components/Triggers.vue'
import { getColorsList, defaultState, numberToHex } from '~/util/util'

const getHash = () => {
    const hash = decodeURI(window.location.hash)

    if (hash) {
      const stateKeysArray = Object.keys(defaultState)
      const hashValuesArray = hash.substring(1, hash.length).split('/')

      const getHashObject = () => {
        var hashObject:any = {}
        stateKeysArray.forEach((key, i) => hashObject[key] = hashValuesArray[i])

        return hashObject
      }

      return getHashObject()
    }

    return null
}

const initialState = getHash() || defaultState

const mainColor = ref<string>(initialState.mainColor)
function setMainColor(arg:string){
  mainColor.value = arg
}

const r = ref<number>(initialState.r)
function setR(arg:number){
  r.value = arg
}

const g = ref<number>(initialState.g)
function setG(arg:number){
  g.value = arg
}

const b = ref<number>(initialState.b)
function setB(arg:number){
  b.value = arg
}

const darkColorsAmount = ref<number>(initialState.darkColorsAmount)
function setDarkColorsAmount(arg:number){
  darkColorsAmount.value = arg
}

const darkestAmount = ref<number>(initialState.darkestAmount)
function setDarkestAmount(arg:number){
  darkestAmount.value = arg
}

const darkColorsMixRotate = ref<number>(initialState.darkColorsMixRotate)
function setDarkColorsMixRotate(arg:number){
  darkColorsMixRotate.value = arg
}

const lightColorsAmount = ref<number>(initialState.lightColorsAmount)
function setLightColorsAmount(arg:number){
  lightColorsAmount.value = arg
}

const lightestAmount = ref<number>(initialState.lightestAmount)
function setLightestAmount(arg:number){
  lightestAmount.value = arg
}

const lightColorsMixRotate = ref<number>(initialState.lightColorsMixRotate)
function setLightColorsMixRotate(arg:number){
  lightColorsMixRotate.value = arg
}

const lightSaturation = ref<number>(initialState.lightSaturation)
function setLightSaturation(arg:number){
  lightSaturation.value = arg
}

const darkSaturation = ref<number>(initialState.darkSaturation)
function setDarkSaturation(arg:number){
  darkSaturation.value = arg
}

const bgColor = ref<string>(initialState.bgColor)
function setBgColor(arg:string){
  bgColor.value = arg
}

if(getHash()) {
  window.location.hash = encodeURI(Object.values(getHash()).join('/'))
}

const darkColors = ref(getColorsList(darkColorsAmount.value, darkestAmount.value, 'black', darkColorsMixRotate.value, darkSaturation.value, mainColor.value).reverse().map((color) => (color)))
const lightColors = getColorsList(lightColorsAmount.value, lightestAmount.value, 'white', lightColorsMixRotate.value, lightSaturation.value, mainColor.value).reverse().map((color) => (color))

</script>

<template>
  <div class="main">
    <!-- main wrapper -->
    <div class="main-wrapper">
      <!-- top section -->
      <div class="top-section">
        <!-- colors section -->
        <div class="w-1/1">
          <!-- global config section -->
          <div class="global-config-section">
            <!-- main color selector -->
            <div>
              <MainColorSelector :main-color="mainColor" :r="r" :g="g" :b="b"/>
            </div>
            <!-- background selector section -->
            <div class="background-selector-section">
              <BackgroundSelector
               :dark-colors="darkColors"
               :light-colors="lightColors"
               :light-colors-amount="lightColorsAmount"
               @set-bg-color="setBgColor"
              />
            </div>
            <!-- triggers section -->
            <div class="triggers-section">
              <Triggers></Triggers>
            </div>
          </div>
          <ColorsRow
           :main-color="mainColor"
           :dark-colors="darkColors"
           :light-colors="lightColors"
          />
          <!-- inputs row -->
          <div class="inputs-row">
            <!-- inputs row item -->
            <div class="mr-40px shrink-0 w-96px">
              <DynamicInput
               :color="numberToHex(mainColor)"
               v-model="darkColorsAmount"
               type="number"
               :min="0"
               :withSlider="false"
               label='Dark colors amount'
              />
            </div>
            <!-- inputs row item -->
            <div class="mr-40px shrink-0 w-96px">
              <DynamicInput
               withSlider
               :color="numberToHex(mainColor)"
               v-model="darkestAmount"
               type="number"
               sufix='%'
               :min="0"
               :max="99"
               label='Darkness'
              />
            </div>
            <!-- inputs row item -->
            <div class="mr-40px shrink-0 w-96px">
              <DynamicInput
               withSlider
               :color="numberToHex(mainColor)"
               v-model="darkColorsMixRotate"
               type="number"
               sufix='º'
               :min="-360"
               :max="360"
               label='Dark colors hue angle'
              />
            </div>
            <!-- inputs row item -->
            <div class="mr-40px shrink-0 w-96px">
              <DynamicInput
               withSlider
               :color="numberToHex(mainColor)"
               v-model="darkSaturation"
               type="number"
               sufix='%'
               :min="-100"
               :max="100"
               label='Dark colors saturation'
              />
            </div>
            <!-- inputs row item separataor -->
            <div class="inputsR-rowI-item-separataor"/>
            <!-- inputs row item -->
            <div class="mr-40px shrink-0 w-96px">
              <DynamicInput
               :color="numberToHex(mainColor)"
               v-model="lightColorsAmount"
               type="number"
               :min="0"
               label='Light colors amount'
              />
            </div>
            <!-- inputs row item -->
            <div class="mr-40px shrink-0 w-96px">
              <DynamicInput
               with-slider
               :color="numberToHex(mainColor)"
               v-model="lightestAmount"
               type="number"
               sufix="%"
               :min="0"
               :max="99"
               label='Lightness'
              />
            </div>
            <!-- inputs row item -->
            <div class="mr-40px shrink-0 w-96px">
              <DynamicInput
               with-slider
               :color="numberToHex(mainColor)"
               v-model="lightColorsMixRotate"
               type="number"
               sufix='º'
               :min="-360"
               :max="360"
               label='Light colors hue angle'
              />
            </div>
            <!-- inputs row item -->
            <div class="mr-40px shrink-0 w-96px">
              <DynamicInput
               with-slider
               :color="numberToHex(mainColor)"
               v-model="lightColorsMixRotate"
               type="number"
               sufix='%'
               :min="-100"
               :max="100"
               label='Light colors saturation'
              />
            </div>
          </div>
        </div>
      </div>
    </div>
    <Footer />
  </div>

</template>

<style scoped>
.main-wrapper{
  flex: 1 1 0%;
  display: flex;
  -webkit-box-align: center;
  align-items: center;
}
.top-section{
  flex: 1;
  display: flex;
  align-items: center;
}
.global-config-section{
  display: flex;
  margin-bottom: 64px;

  flex-wrap: wrap;
    @media (max-width: 1100px) {
  }
}
.background-selector-section{
  border-left: 1px solid var(--border);
  padding: 0 48px;
  height: 160px;

  @media (max-width: 720px) {
    padding: 16px 0;
    margin-top: 16px;
    border-left: 0;
    border-top: 1px solid var(--border);
  }
}
.main{
  padding: 40px 80px;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}
.triggers-section{
  border-left: 1px solid var(--border);
  padding: 0 48px;

  @media (max-width: 720px) {
    padding: 16px 0;
    margin-top: 16px;
    border-left: 0;
    border-top: 1px solid var(--border);
  }
}
.inputs-row{
  display: flex;
  width: 100%;
  margin-bottom: var(--space-xl);

  @media (max-width: 720px) {
    flex-direction: column;
  }
}
.inputsR-rowI-item-separataor{
  margin-right: 48px;
  display: block;
  width: 1px;
  flex-shrink: 0;
  background-color: var(--border);
}
</style>
