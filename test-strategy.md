##Cambios a realizar en el codigo
1. El número a adivinar debe pertenecer al conjunto de los enteros:
En el código original, el número aleatorio se generaba como un número flotante, lo que significa que el número a adivinar no necesariamente sería un número entero. Para solucionar esto, es necesario modificar la línea que genera el número aleatorio para que genere un número entero en lugar de un número flotante:
Reemplazamos
let randomNumber = Math.random() * 10;
Por:
let randomNumber = Math.floor(Math.random() * 100) + 1;

Asi el numero aleatorio estará entre 1 y 100. Y si y solo si sera un número entero.


2. El número que ingrese el jugador debe pertenecer al conjunto de los enteros:
En el código original, no se verifica si el número ingresado por el jugador es un número entero o no. Para asegurarse de que el número ingresado sea un número entero, se debe agregar una validación en la función checkGuess().
Reemplazamos
let userGuess = guessField.value;
Por:
let userGuess = parseInt(guessField.value);
if(isNaN(userGuess)) {
    alert("Ingresa un número entero válido.");
    return;
}

Con esta modificación nos aseguramos que el usuario ingrese un número entero en caso contrario nos mostrará una alerta y no contará como un intento

3. Mostrar un mensaje de retroalimentación para el jugador:
En el código original, no se proporciona una retroalimentación clara al jugador si el número ingresado es mayor o menor que el número a adivinar. Para solucionar esto, se deben agregar mensajes de retroalimentación que indiquen si el número ingresado es mayor o menor que el número a adivinar.

Vamos a reemplazar:

if(userGuess === randomNumber) {
  lastResult.textContent = '!!!Pérdistes!!!';
  lastResult.style.backgroundColor = 'black';
  lowOrHi.textContent = '';
  setGameOver();
} else if(guessCount === ATTEMPS) {
  lastResult.textContent = 'Felicitaciones! adivinaste el número!';
  lastResult.style.backgroundColor = 'red';
  setGameOver();
} else {
  lastResult.textContent = 'Incorrecto! ';
  lastResult.style.backgroundColor = 'green';
}


Por:

if(userGuess === randomNumber) {
    lastResult.textContent = 'Felicitaciones! Adivinaste el número!';
    lastResult.style.backgroundColor = 'green';
    lowOrHi.textContent = '';
    setGameOver();
} else if(guessCount === ATTEMPS) {
    lastResult.textContent = '!!!Pérdistes!!! El número era ' + randomNumber;
    lastResult.style.backgroundColor = 'red';
    setGameOver();
} else {
    lastResult.textContent = 'Incorrecto! ';
    lastResult.style.backgroundColor = 'black';
    if(userGuess < randomNumber) {
        lowOrHi.textContent = 'El número es mayor!';
    } else if(userGuess > randomNumber) {
        lowOrHi.textContent = 'El número es menor!';
    }
}

5. El juego actualmente permite que el usuario continue ingresando valores despues de 10 intentos
Para solucionar esto se debe desactivar el campo de entrada de texto y el botón de envío despues de que se alcancen los 10 intentos o si el usuario adivina el número.

Por último, hay algunos errores en el código actual que deben ser corregidos para que el juego funcione correctamente. Por ejemplo, en la línea 32, falta un punto antes de "lowOrHi", lo que hace que el programa no encuentre el elemento correspondiente en el documento HTML. Además, en la línea 51, "addeventListener" debe ser reemplazado por "addEventListener"