
// Dark Tech main JS
document.addEventListener('DOMContentLoaded', function(){
  // GSAP intro animation
  if (typeof gsap !== 'undefined'){
    gsap.from('.brand h1', {y:-10, opacity:0, duration:0.8, ease:'power2.out'});
    gsap.from('.nav a', {y:-6, opacity:0, duration:0.8, stagger:0.08, delay:0.1});
    gsap.from('.hero-inner', {y:10, opacity:0, duration:0.9, delay:0.2});
  }

  // Floating background subtle movement
  let bg = document.getElementById('bg');
  let m = 0;
  setInterval(()=>{
    m += 0.2;
    bg.style.transform = 'translateY(' + Math.sin(m)/6 + 'vh) scale(1.02)';
  },90);

  // Quiz logic if on tests page
  const checkBtn = document.getElementById('checkBtn');
  const showKey = document.getElementById('showKey');
  const resultBox = document.getElementById('result');
  if (checkBtn){
    checkBtn.addEventListener('click', function(){
      // correct answers array (indexes)
      const key = [1,1,1,1,0,1,1,1,1,1,1,1,1,1,1,0,0,0,1,0];
      let total = key.length;
      let score = 0;
      for (let i=0;i<total;i++){
        let qname = 'q'+(i+1);
        let els = document.getElementsByName(qname);
        let chosen = -1;
        for (let el of els){ if (el.checked) chosen = parseInt(el.value); }
        if (chosen === key[i]) score++;
      }
      resultBox.textContent = 'Результат: ' + score + ' / ' + total;
      // feedback color
      if (score/total >= 0.9) resultBox.style.color = '#88ffb3';
      else if (score/total >= 0.6) resultBox.style.color = '#ffd966';
      else resultBox.style.color = '#ff6b6b';
    });

    showKey.addEventListener('click', function(){
      const key = [1,1,1,1,0,1,1,1,1,1,1,1,1,1,1,0,0,0,1,0];
      // show correct answers by highlighting labels
      for (let i=0;i<key.length;i++){
        let q = document.getElementsByName('q'+(i+1));
        for (let el of q){
          let lab = el.parentNode;
          lab.style.background = 'transparent';
          if (parseInt(el.value) === key[i]){
            lab.style.background = 'linear-gradient(90deg, rgba(0,230,255,0.06), rgba(0,0,0,0.02))';
            lab.style.borderLeft = '3px solid rgba(0,230,255,0.18)';
            lab.style.paddingLeft = '8px';
          }
        }
      }
    });
  }
});
