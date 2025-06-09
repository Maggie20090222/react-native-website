npm install -g expo-cli
npx create-expo-app my-focus-app
cd my-focus-app
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';
import SuggestionScreen from './screens/SuggestionScreen';

const Stack = createNativeStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen name="建議活動" component={SuggestionScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
import React, { useState } from 'react';
import { View, Text, Button, StyleSheet } from 'react-native';
import suggestions from '../data/suggestions';

export default function SuggestionScreen() {
  const [currentSuggestion, setCurrentSuggestion] = useState(getRandomSuggestion());

  function getRandomSuggestion() {
    const index = Math.floor(Math.random() * suggestions.length);
    return suggestions[index];
  }

  function handleNext() {
    setCurrentSuggestion(getRandomSuggestion());
  }

  return (
    <View style={styles.container}>
      <Text style={styles.title}>今天你可以試試：</Text>
      <Text style={styles.suggestion}>{currentSuggestion}</Text>
      <Button title="換一個建議" onPress={handleNext} />
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: 'center', alignItems: 'center', padding: 20 },
  title: { fontSize: 22, marginBottom: 20 },
  suggestion: { fontSize: 20, color: '#555', marginBottom: 30, textAlign: 'center' }
});
const suggestions = [
  "去陽台呼吸新鮮空氣 5 分鐘",
  "做 10 次深呼吸",
  "泡杯熱茶或熱水",
  "散步 10 分鐘",
  "寫下今天的三件感謝小事",
  "做幾個伸展動作",
  "閱讀 5 頁書",
  "聽一首輕鬆的音樂",
  "打給一個朋友問候一下",
  "坐下來靜坐 3 分鐘"
];

export default suggestions;
npx expo start
