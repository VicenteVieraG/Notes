# Notas
Breve guía de nuevas funciones de las extendiones de markdown.
## Checkboxes
- [ ] Esto es una checkbox vacía.
- [x] Esto es una checkbox llena.
## Links
Los links se declaran como si fueran variables. Se les pueden asignar valores de links de todo tipo, tales como links a páginas web, referencias a elementos dentro del mismo documento o incluso hacer referencia a otros documentos. Se escriben de la siguiente forma:
>[Nombre_de_La_Variable]: Link .

Para utilizar la variable basta con la siguiente sintáxis:
>[Texto][[Nombre de la variable]]

La misma sintáxis se usa para hacer referencias a elementos dentro del mismo documento:
>[Texto](Nivel en la jerarquía del elemento a seleccionar(#,##,###,...)Texto del elemento a seleccionar)

No se pueden declarar dentro de un párrafo o si no se tiene un salto de linea de separación de un párrafo.
## Notas de Pie de Página
Estas sirven para crear referencias hacia definiciones dentro del mismo documento:
Condepto al que se le quiere agar una definición:
Texto[^1]

Declaración de la definición: (Ver en __Markdown__)
>[^1]: Link
## Dependencias Instaladas
- Markdown All in One
- Markdown Checkboxes
- Markdown Emoji
- Markdown Footnotes
- Markdown Preview Mermaid Support
- Mermaid Markdown Syntax Highlighting