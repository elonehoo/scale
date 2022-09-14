<script setup lang="ts">
import { ref } from 'vue'
import Footer from '~/component/Footer.vue'
import Title from '~/components/Title.vue'
import MainColorLabel from '~/components/MainColorLabel.vue'
import MainColorInput from './components/MainColorInput.vue'
import Label from './components/Label.vue'
import Range from './components/Range.vue'
import { getColorsList, defaultState, numberToHex,isValidHex,hexToNumber,errorColor } from '~/util/util'
import Color from 'color'

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

let mainColor = ref<string>(initialState.mainColor)
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

const currentState = {
    darkColorsAmount,
    lightColorsAmount,
    darkestAmount,
    lightestAmount,
    darkColorsMixRotate,
    lightColorsMixRotate,
    lightSaturation,
    darkSaturation,
    mainColor,
    r,
    g,
    b,
    bgColor,
}

const updateHash = ()=>{
  window.location.hash = encodeURI(Object.values(currentState).join('/'))
}

const updateThemeColor = () => {
  document.getElementById('themeMetaTag')?.setAttribute('content', numberToHex(mainColor))
}

const updateRgbWithMainColor = (color:any) => {
  if (isValidHex(numberToHex(color))) {
    setR(Color(numberToHex(color)).rgb().red())
    setG(Color(numberToHex(color)).rgb().green())
    setB(Color(numberToHex(color)).rgb().blue())
  }
}

const handleMainColorChange = (e:any) => {
  let typedColorFiltered
  const typedColor = e

  if (typedColor[0] === '#') {
    typedColorFiltered = typedColor.substr(1, typedColor.length)
  } else {
    typedColorFiltered = typedColor
  }

  setMainColor(typedColorFiltered)

  updateRgbWithMainColor(typedColorFiltered)
}

const rgbToMainColor = () => {
  setTimeout(() => {
    setMainColor(hexToNumber(Color(`rgb(${r.value}, ${g.value}, ${b.value})`).hex()))
  }, 0)
}

function handleRChange(value:number){
  setR(value)
  rgbToMainColor()
}

const handleGChange = (value:number) => {
  setG(value)
  rgbToMainColor()
}

const handleBChange = (value:number) => {
  setB(value)
  rgbToMainColor()
}

const bgRefToNumber = (ref:any) => {
  if(ref.includes('l-')) {
    return ref.substring(2, ref.length)
  }
  if(ref.includes('d-')) {
    return ref.substring(2, ref.length)
  }
}

const setBgColorVar = () => {
  let color = ''
  if(bgColor === undefined) {
    color = defaultState.bgColor
    setBgColor(defaultState.bgColor)
  } else {
    if(bgColor.value === 'white' || bgColor.value === 'black') {
      color = bgColor.value
    }

    if(bgColor.value.includes('l-')) {
      color = lightColors[lightColorsAmount.value - bgRefToNumber(bgColor.value)]
    }

    if(bgColor.value.includes('d-')) {
      color = darkColors.value[bgRefToNumber(bgColor.value)]
    }
  }
  document.documentElement.style.setProperty('--bodyBg', color)
}

setBgColorVar()

const setBodyColorVar = () => {
  const givenColor = isValidHex(numberToHex(mainColor.value)) ? numberToHex(mainColor.value) : errorColor

  const getMixColor = () => {
    if(bgColor.value) {
      if(bgColor.value.includes('l-') || bgColor.value.includes('white')) {
        return 'black'
      } else {
        return 'white'
      }
    } else {
      return 'white'
    }
  }
  const bodyColor = Color(givenColor).mix(Color(getMixColor()), 0.5).string()
  const bodyDimmed = Color(givenColor).mix(Color(getMixColor()), 0.5).fade(0.7).string()
  const bodyXDimmed = Color(givenColor).mix(Color(getMixColor()), 0.5).fade(0.9).string()
  document.documentElement.style.setProperty('--bodyColor', bodyColor)
  document.documentElement.style.setProperty('--bodyDimmed', bodyDimmed)
  document.documentElement.style.setProperty('--bodyXDimmed', bodyXDimmed)
  document.documentElement.style.setProperty(
    '--border',
    isValidHex(numberToHex(mainColor.value)) ? Color(numberToHex(mainColor.value)).mix(Color(getMixColor()), 0.3).fade(0.85).string() : '#ddd'
  )
}

setBodyColorVar()

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
            <div class="mr-40px">
              <!-- main color selector -->
              <div>
                <Title>Color</Title>
                <div class="flex mb-16px">
                  <MainColorLabel />
                  <MainColorInput v-model="mainColor"/>
                </div>
              </div>
              <div class="flex items-center">
                <Label>R</Label>
                <Range v-model="r" :min="0" :max="255"/>
              </div>
              <div class="flex items-center">
                <Label>G</Label>
                <Range v-model="g" :min="0" :max="255"/>
              </div>
              <div class="flex items-center">
                <Label>B</Label>
                <Range v-model="b" :min="0" :max="255"/>
              </div>
            </div>
            <!-- background selector section -->
            <div class="background-selector-section">
              <!-- background selector -->
            </div>
            <!-- triggers section -->
            <div class="triggers-section">
              <!-- triggers -->
            </div>
          </div>
          <!-- colors row -->
          <!-- inputs row -->
          <div class="inputs-row">
            <!-- inputs row item -->
            <div class="mr-40px shrink-0 w-96px">
              <!-- dynamic input -->
            </div>
            <!-- inputs row item -->
            <div class="mr-40px shrink-0 w-96px">
              <!-- dynamic input -->
            </div>
            <!-- inputs row item -->
            <div class="mr-40px shrink-0 w-96px">
              <!-- dynamic input -->
            </div>
            <!-- inputs row item -->
            <div class="mr-40px shrink-0 w-96px">
              <!-- dynamic input -->
            </div>
            <!-- inputs row item separataor -->
            <div class="inputsR-rowI-item-separataor"/>
            <!-- inputs row item -->
            <div class="mr-40px shrink-0 w-96px">
              <!-- dynamic input -->
            </div>
            <!-- inputs row item -->
            <div class="mr-40px shrink-0 w-96px">
              <!-- dynamic input -->
            </div>
            <!-- inputs row item -->
            <div class="mr-40px shrink-0 w-96px">
              <!-- dynamic input -->
            </div>
            <!-- inputs row item -->
            <div class="mr-40px shrink-0 w-96px">
              <!-- dynamic input -->
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
