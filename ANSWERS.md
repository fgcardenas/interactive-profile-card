# Preguntas de checkpoint

1. **`onPress={handlePress}` y no `onPress={handlePress()}`.** `onPress` espera una función que React Native llamará más tarde, cuando el usuario presione. `handlePress()` ejecuta la función inmediatamente durante el render y le pasa su resultado (normalmente `undefined`) a `onPress`, por lo que al presionar no ocurre nada.

2. **`Button` vs `Pressable`.** `Button` es un componente listo, con el estilo de cada plataforma, que solo acepta `title`, `color`, `onPress` y `disabled`; no tiene `style` ni admite hijos personalizados. `Pressable` envuelve cualquier contenido y da control total sobre el diseño y el feedback. Uso `Button` para acciones rápidas y estándar, y `Pressable` cuando el diseño es propio.

3. **Función `style` de `Pressable`.** Recibe un objeto con el estado de la interacción (por ejemplo `{ pressed }`) y devuelve un estilo o un arreglo de estilos. Ejemplo: `style={({ pressed }) => [styles.button, pressed && styles.pressed]}` hace que el botón quede semitransparente mientras se mantiene presionado.

4. **Cambiar el estado directamente.** Asignar `isFollowing = true` no le avisa a React que algo cambió, así que el componente no se vuelve a renderizar y el valor se pierde en el siguiente render. En su lugar se llama al setter, `setIsFollowing(true)`, que programa un nuevo render con el valor actualizado.

5. **`followers` no es un segundo `useState`.** Se puede calcular a partir de `isFollowing` (`BASE_FOLLOWERS + (isFollowing ? 1 : 0)`), por lo que es un *valor derivado*. Guardarlo en otro estado duplicaría información y ambos valores podrían quedar desincronizados.

6. **Input controlado.** Un `TextInput` controlado toma su texto del estado de React, de modo que el estado es la única fuente de verdad. Lo controlan dos props: `value={message}` y `onChangeText={setMessage}`, que actualiza el estado en cada cambio.

7. **`selectedSkills.push(skill)` es incorrecto.** Muta el arreglo que vive en el estado, así que React puede no detectar el cambio y la interfaz no se actualiza. El código correcto es `setSelectedSkills([...selectedSkills, skill])` para agregar y `setSelectedSkills(selectedSkills.filter((item) => item !== skill))` para quitar.
