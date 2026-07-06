<!DOCTYPE html>
<html>
  <head>
    <script src="https://aframe.io/releases/1.5.0/aframe.min.js"></script>
    <script>
      AFRAME.registerComponent('cervello-autonomo', {
        init: function () {
          this.timer = 0;
          this.stati = ['calmo', 'curioso', 'glitch'];
          this.statoAttuale = 'calmo';
        },
        tick: function (time, timeDelta) {
          this.timer += timeDelta;
          if (this.timer >= 3000) {
            this.timer = 0;
            let indiceCasuale = Math.floor(Math.random() * this.stati.length);
            this.statoAttuale = this.stati[indiceCasuale];
            let el = this.el;
            if (this.statoAttuale === 'calmo') {
              el.setAttribute('animation', 'property: position; to: 0 1.8 -3; dur: 1500; easing: easeInOutQuad');
            } 
            else if (this.statoAttuale === 'curioso') {
              let randomX = (Math.random() * 2) - 1;
              el.setAttribute('animation', 'property: position; to: ' + randomX + ' 1.5 -3; dur: 2000; easing: easeInOutSine');
            } 
            else if (this.statoAttuale === 'glitch') {
              el.setAttribute('animation', 'property: rotation; to: 0 360 0; dur: 800; easing: linear');
            }
          }
        }
      });
    </script>
  </head>
  <body>
    <a-scene>
      <a-sky color="#000000"></a-sky>
      
      <a-entity geometry="primitive: plane; width: 100; height: 100" rotation="-90 0 0" material="color: #ffffff; wireframe: true;"></a-entity>
      
      <a-box id="entita-autonoma" position="0 1.5 -3" color="#ff0000" cervello-autonomo></a-box>

      <a-entity camera look-controls position="0 1.6 0"></a-entity>
    </a-scene>
  </body>
</html>
