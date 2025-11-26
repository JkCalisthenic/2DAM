- --
- Tags: #Proyecto #Clase #Framework #ReactNative #Typescript #LenguajeDeProgramación 
- --
# 1. Componentes
- View -> Equivalente a un Div
- Text -> Para mostrar texto
- Button -> Un botón
- Image -> Imágenes
- TextInput -> Campos de texto
- ScrollView -> Scroll
- FlatList ->Listas optimizadas

Ejemplos:
``` tsx
import { View, Text } from "react-native";

export default function App() {
  return (
    <View>
      <Text>Hola desde React Native</Text>
    </View>
  );
}
```

# 2. Estilos
React Native usa un sistema de estilos basado en Flexbox.
``` tsx
<View style={{ backgroundColor: 'lightblue', padding: 20 }}>
  <Text style={{ fontSize: 20 }}>Hola</Text>
</View>
```
Los estilos son objetos de JS, no clases CSS

# 3. Props
Los props son la forma de pasar datos de un componente padre a uno hijo.
Piensa en ellos como parámetros de un método o argumentos de un constructor.

Al crear una función e te devuelve un fragmento de código y esta funcion necesita algún parámetro se le pasa como argumento, esto se le llama prop.
```tsx
function Saludo({ nombre }) {
  return <Text>Hola, {nombre}</Text>;
}

<Saludo nombre="Jk" />
```
- Saludo es un componente "función" que recibe un nombre {nombre}.
- Cuando lo usas en el padre con nombre="Jk", el hijo recibe ese valor.
- Inmutable: el hijo no debería cambiar los props.

# 4. Estado (useState)
El estado es la información que cambia durante la vda del componente y que hace que la interfáz se actualice automáticamente
```tsx
import { useState } from "react";

function Contador() {
  const [numero, setNumero] = useState(0); // estado inicial 0

  return (
    <View>
      <Text>{numero}</Text>
      <Button title="Sumar" onPress={() => setNumero(numero + 1)} />
    </View>
  );
}

```
- numero -> valor actual
- setNumero -> función para cambiarlo
- Cada vez que llamas a setNumero, React Native re-renderiza el componente con el nuevo valor.

# 5. Hooks
Un hook es una función especial que permite "engancharse" al ciclo de vida de un componente funcional.

El más usado aparte de useState es useEffect.
1. useState -> guardar valores que cambian (estado)
2. useEffect -> ejecutar código después de renderizar o cuando cambian ciertas variables.
	- Ejemplo: pedir datos a una API, escuchar un evento, usar un temporizador.

Los hooks no son solo para estado, sino para controlar efectos secundarios o comportamientos del componente.
```tsx
import { useEffect } from "react";

useEffect(() => {
  console.log("El componente se montó");

  return () => {
    console.log("El componente se va a desmontar");
  };
}, []); // [] = se ejecuta solo al inicio y al desmontar
```
- Se ejecuta después de renderizar.
- Sirven para llamar APIs, suscribirse a eventos, limpiar, timers.
- \[\] significa "solo al montar/desmontar".
- \[valor\] significa "ejecutar cada vex que valor cambie".  

# 6. Navegación
En móviles no hay "páginas web", hay pantallas. Para moverse entre ellas se usan stacks (apilar pantallas) o tabs.

Ejemplo básico con React Navigation:
```tsx
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';
import { Button, Text, View } from 'react-native';

function Home({ navigation }) {
  return (
    <View>
      <Text>Pantalla Home</Text>
      <Button title="Ir a Detalle" onPress={() => navigation.navigate('Detalle')} />
    </View>
  );
}

function Detalle() {
  return (
    <View>
      <Text>Pantalla Detalle</Text>
    </View>
  );
}

const Stack = createNativeStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen name="Home" component={Home}/>
        <Stack.Screen name="Detalle" component={Detalle}/>
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```
- navigation.navigate('Detalle) -> cambia a la pantalla Detalle.
- Cada pantalla recibe navigation como prop automáticamente.
- Stack = aplicar pantallas -> "volver" elimina la pantalla de arriba.

