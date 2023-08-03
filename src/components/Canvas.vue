<template>
  <div id="preloader"> </div>
  <canvas id="canvas" ref="canvas" width="1000" height="675"></canvas>
</template>

<script>
function getRandomArbitrary(min, max) {
  return Math.floor(Math.random() * (max - min) + min);
}

export default {
  mounted() {
    this.drawCanvas();
  },
  methods: {
    async preloadCustomFonts() {
      const aAnotherTag = new FontFace(
        'aAnotherTag',
        `url('/assets/fonts/aAnotherTag.ttf') format('truetype')`
      );
      const adrip1 = new FontFace(
        'adrip1',
        `url('/assets/fonts/adrip1.ttf') format('truetype')`
      );
      const Mostwasted = new FontFace(
        'Mostwasted',
        `url('/assets/fonts/Mostwasted.ttf') format('truetype')`
      );
      const Painterz = new FontFace(
        'Painterz',
        `url('/assets/fonts/Painterz.ttf') format('truetype')`
      );
      const RuthlessDrippin1 = new FontFace(
        'RuthlessDrippin1',
        `url('/assets/fonts/RuthlessDrippin1.ttf') format('truetype')`
      );
      const RuthlessWreckin1 = new FontFace(
        'RuthlessWreckin1',
        `url('/assets/fonts/RuthlessWreckin1.ttf') format('truetype')`
      );

      await Promise.all([
        aAnotherTag.load(),
        adrip1.load(),
        Mostwasted.load(),
        Painterz.load(),
        RuthlessDrippin1.load(),
        RuthlessWreckin1.load()
      ]);

      console.log('Fonts loaded');
    },
    async drawCanvas() {
      const canvas = this.$refs.canvas;
      const context = canvas.getContext('2d');
      const fonts = [
        'aAnotherTag',
        'adrip1',
        'Mostwasted',
        'Painterz',
        'RuthlessDrippin1',
        'RuthlessWreckin1'
      ];

      await this.preloadCustomFonts();

      // Draw header block
      context.beginPath();
      context.strokeStyle = 'red'; // Set line color to red
      context.lineWidth = 400; // Set line width
      const headerYPosition = 0; // Y-coordinate of the line (in this case, the center of the canvas)
      context.moveTo(0, headerYPosition); // Start drawing from the left edge
      context.lineTo(1000, headerYPosition); // Draw the line to the right edge
      context.stroke(); // Actually draw the line

      // Draw footer block
      context.beginPath();
      context.strokeStyle = 'red'; // Set line color to red
      context.lineWidth = 200; // Set line width
      const footerYPosition = 675; // Y-coordinate of the line (in this case, the center of the canvas)
      context.moveTo(0, footerYPosition); // Start drawing from the left edge
      context.lineTo(1000, footerYPosition); // Draw the line to the right edge
      context.stroke(); // Actually draw the line

      // Set font and text properties
      const bigFontSize = 100;
      const smallFontSize = 36;
      const customFontSize = 250;
      context.font = `bold ${bigFontSize}px Arial`; // Set font and size for "Hello"
      context.fillStyle = 'white'; // Set fill color to white
      context.textAlign = 'center'; // Center the text horizontally
      context.fontWeight = 'bold';

      // Draw "Hello" in the center of the canvas
      const xPosition = canvas.width / 2;
      const helloYPosition = 170 - bigFontSize / 2;
      context.fillText('Hello', xPosition, helloYPosition);

      // Draw "my name is" right below "Hello"
      context.font = `bold ${smallFontSize}px Arial`; // Set font and size for "my name is"
      const myNameIsYPosition = 180 - smallFontSize / 2;;
      context.fillText('my name is', xPosition, myNameIsYPosition);


      // Draw Custom Text
      const fontToUse = fonts[getRandomArbitrary(0, fonts.length - 1)];
      context.font = `${customFontSize}px ${fontToUse}, Arial`; // Use the custom font along with a fallback font
      const customTextYPosition = 550 - customFontSize / 2;
      context.fillStyle = 'black'; // Set fill color to white
      context.fillText('Cmatias', xPosition, customTextYPosition);
    }
  }
};
</script>

<style>
@font-face {
  font-family: "aAnotherTag";
  src: local("aAnotherTag"),
   url(../../assets/fonts/aAnotherTag.ttf) format("truetype");
}

@font-face {
  font-family: "adrip1";
  src: local("adrip1"),
   url(../../assets/fonts/adrip1.ttf) format("truetype");
}

@font-face {
  font-family: "Mostwasted";
  src: local("Mostwasted"),
   url(../../assets/fonts/Mostwasted.ttf) format("truetype");
}

@font-face {
  font-family: "Painterz";
  src: local("Painterz"),
   url(../../assets/fonts/Painterz.ttf) format("truetype");
}

@font-face {
  font-family: "RuthlessDrippin1";
  src: local("RuthlessDrippin1"),
   url(../../assets/fonts/RuthlessDrippin1.ttf) format("truetype");
}

@font-face {
  font-family: "RuthlessWreckin1";
  src: local("RuthlessWreckin1"),
   url(../../assets/fonts/RuthlessWreckin1.ttf) format("truetype");
}

#preloader {
  font-family: 'aAnotherTag', 'adrip1', 'Mostwasted', 'Painterz', 'RuthlessDrippin1', 'RuthlessWreckin1';
}

#canvas {
  background-color: white;
  border-radius: 50px;
}
</style>