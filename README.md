# Desarrollo_Movil
App.js


import React, { useState } from 'react';
import { Text, TextInput, Button, View, StyleSheet, TouchableOpacity, Image } from 'react-native';

export default function App() {
  const [numero1, setNumero1] = useState('');
  const [numero2, setNumero2] = useState('');
  const [resultado, setResultado] = useState(null);

  const operar = (operacion) => {
    const num1 = parseFloat(numero1);
    const num2 = parseFloat(numero2);
    if (!isNaN(num1) && !isNaN(num2)) {
      let res;
      if (operacion === 'sumar') res = num1 + num2;
      else if (operacion === 'restar') res = num1 - num2;
      else if (operacion === 'multiplicar') res = num1 * num2;
      else if (operacion === 'dividir') {
        if (num2 === 0) {
          setResultado('No se puede dividir por cero');
          return;
        }
        res = num1 / num2;
      }
      setResultado(res);
    } else {
      setResultado('Por favor ingrese números válidos');
    }
  };

  return (
    <View style={styles.container}>
      <Text style={styles.header}>Calculadora básica</Text>
      <TextInput
        style={styles.input}
        keyboardType="numeric"
        placeholder="Ingresa el primer número"
        value={numero1}
        onChangeText={setNumero1}
      />
      <TextInput
        style={styles.input}
        keyboardType="numeric"
        placeholder="Ingresa el segundo número"
        value={numero2}
        onChangeText={setNumero2}
      />

      <View style={styles.buttonsRow}>
        <Button onPress={() => operar('sumar')} title="Sumar" />
        <Button onPress={() => operar('restar')} title="Restar" />
        <Button onPress={() => operar('multiplicar')} title="Multiplicar" />
        <Button onPress={() => operar('dividir')} title="Dividir" />
      </View>

      <TouchableOpacity>
        <Image
          source={{
            uri: 'https://media.istockphoto.com/id/1426692001/vector/cute-funny-halloween-ghost-scary-design-illustration-childish-spooky-boo-character-for-kids.jpg?s=1024x1024&w=is&k=20&c=C-CII0FQnRliKvCTctwQvjWQWGS-WBcxGcrOfBBTets='
          }}
          style={styles.operatorImage}
        />
      </TouchableOpacity>

      {resultado !== null && (
        <Text style={styles.result}>Resultado: {resultado}</Text>
      )}
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    padding: 20,
  },
  header: {
    fontSize: 24,
    marginBottom: 20,
  },
  input: {
    height: 40,
    borderColor: 'gray',
    borderWidth: 1,
    marginBottom: 10,
    width: '100%',
    paddingLeft: 10,
    fontSize: 18,
  },
  result: {
    marginTop: 20,
    fontSize: 20,
    fontWeight: 'bold',
  },
  operatorImage: {
    width: 50,
    height: 50,
    backgroundColor: 'green',
    borderRadius: 100,
  },
  buttonsRow: {
    flexDirection: 'row',
    flexWrap: 'wrap',
    justifyContent: 'space-between',
    gap: 10,
    marginVertical: 10,
  },
});
