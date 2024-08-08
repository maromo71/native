# Exercício: Criando uma Calculadora em React Native

## Introdução
Neste exercício, vamos criar uma calculadora simples utilizando React Native. 
Este composição em React Native. A calculadora terá botões para números, operações básicas, 
um botão para limpar [C] e um botão para calcular o resultado [=].

## Passo 1: Configuração do Ambiente
Certifique-se de que o ambiente React Native está configurado corretamente. 
Você precisará do Node.js, do Expo CLI e de um simulador ou dispositivo físico.

Execute os seguintes comandos para iniciar um novo projeto:

```bash
npm install -g expo-cli
expo init Calculadora
cd Calculadora
expo start
```

## Passo 2: Estrutura do Projeto
Vamos dividir a calculadora nos seguintes componentes:

1. **Display**: Para mostrar o valor atual no visor.
2. **Keypad**: Para organizar os botões em linhas.
3. **Button**: Para os botões individuais da calculadora.
4. **App**: Componente principal que une todos os componentes e gerencia o estado.

### Criar o Componente Display
Este componente será responsável por exibir o valor atual da calculadora.

```javascript
// components/Display.js
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

const Display = ({ value }) => {
  return (
    <View style={styles.container}>
      <Text style={styles.displayText}>{value}</Text>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    backgroundColor: '#f4f4f4',
    padding: 20,
    justifyContent: 'center',
    alignItems: 'flex-end',
  },
  displayText: {
    fontSize: 40,
    fontWeight: 'bold',
  },
});

export default Display;
```

### Criar o Componente Button
Esse componente representará cada botão.

```javascript
// components/Button.js
import React from 'react';
import { Text, TouchableOpacity, StyleSheet } from 'react-native';

const Button = ({ label, onPress, style }) => {
  return (
    <TouchableOpacity onPress={() => onPress(label)} style={[styles.button, style]}>
      <Text style={styles.buttonText}>{label}</Text>
    </TouchableOpacity>
  );
};

const styles = StyleSheet.create({
  button: {
    backgroundColor: '#f0f0f0',
    flex: 1,
    height: 70,
    justifyContent: 'center',
    alignItems: 'center',
    margin: 5,
    borderRadius: 5,
  },
  buttonText: {
    fontSize: 24,
    fontWeight: 'bold',
  },
});

export default Button;
```

### Criar o Componente Keypad
Este componente será responsável por organizar os botões da calculadora em linhas.

```javascript
// components/Keypad.js
import React from 'react';
import { View, StyleSheet } from 'react-native';
import Button from './Button';

const Keypad = ({ onPress }) => {
  const buttons = [
    ['7', '8', '9', '/'],
    ['4', '5', '6', '*'],
    ['1', '2', '3', '-'],
    ['C', '0', '=', '+'],
  ];

  return (
    <View style={styles.container}>
      {buttons.map((row, rowIndex) => (
        <View key={rowIndex} style={styles.row}>
          {row.map((button) => (
            <Button
              key={button}
              label={button}
              onPress={onPress}
              style={isNaN(button) ? styles.operatorButton : null}
            />
          ))}
        </View>
      ))}
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
  },
  row: {
    flexDirection: 'row',
    justifyContent: 'space-around',
    marginBottom: 10,
  },
  operatorButton: {
    backgroundColor: '#f9a825',
  },
});

export default Keypad;
```

### Atualizar o Componente App
Agora, vamos unir todos os componentes no arquivo App.js.

```javascript
// App.js
import React, { useState } from 'react';
import { View, StyleSheet } from 'react-native';
import Display from './components/Display';
import Keypad from './components/Keypad';

const App = () => {
  const [displayValue, setDisplayValue] = useState('');
  const [operator, setOperator] = useState(null);
  const [firstOperand, setFirstOperand] = useState(null);
  const [waitingForSecondOperand, setWaitingForSecondOperand] = useState(false);

  const handlePress = (value) => {
    if (!isNaN(value)) {
      handleNumber(value);
    } else if (value === 'C') {
      clear();
    } else if (value === '=') {
      calculate();
    } else {
      handleOperator(value);
    }
  };
  

  const handleNumber = (num) => {
    if (waitingForSecondOperand) {
      setDisplayValue(num);
      setWaitingForSecondOperand(false);
    } else {
      setDisplayValue(displayValue === '0' ? num : displayValue + num);
    }
  };

  const handleOperator = (nextOperator) => {
    const inputValue = parseFloat(displayValue);

    if (firstOperand == null && !isNaN(inputValue)) {
      setFirstOperand(inputValue);
    } else if (operator) {
      const result = calculate();
      setDisplayValue(String(result));
      setFirstOperand(result);
    }

    setWaitingForSecondOperand(true);
    setOperator(nextOperator);
  };

  const calculate = () => {
    const secondOperand = parseFloat(displayValue);
  
    if (operator && firstOperand != null && !isNaN(secondOperand)) {
      let result;
  
      switch (operator) {
        case '+':
          result = firstOperand + secondOperand;
          break;
        case '-':
          result = firstOperand - secondOperand;
          break;
        case '*':
          result = firstOperand * secondOperand;
          break;
        case '/':
          result = firstOperand / secondOperand;
          break;
        default:
          return;
      }
  
      setOperator(null);
      setFirstOperand(result);
      setDisplayValue(String(result));  // Update display with the result
      setWaitingForSecondOperand(true); // Prepare for the next input
      return result;
    }
    return displayValue;
  };
  

  const clear = () => {
    setDisplayValue('');
    setOperator(null);
    setFirstOperand(null);
    setWaitingForSecondOperand(false);
  };

  return (
    <View style={styles.container}>
      <Display value={displayValue} />
      <Keypad onPress={handlePress} />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    backgroundColor: '#fff',
  },
});

export default App;
```

## Conclusão
Este exercício demonstra como criar uma calculadora simples em React Native usando 
componentes modulares e gerenciando o estado da aplicação. Isso ajuda a entender a importância 
de dividir a lógica da aplicação em componentes reutilizáveis e bem organizados.

## Pontos de Aprendizado
- **Modularidade**: Dividir a aplicação em componentes menores e reutilizáveis.
- **Reutilização de Componentes**: Criar componentes como Button e Display, que podem ser reutilizados.
- **Gerenciamento de Estado**: Centralizar o gerenciamento de estado no componente App e passar propriedades para os componentes filhos.
- **Composição de Componentes**: Usar componentes filhos (Keypad e Display) dentro de um componente pai (App).
