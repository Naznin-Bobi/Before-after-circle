# Before-after-circle
Customizable Before After Section For Any Theme
<style>
.skin-tint-section {
  text-align: center;
  padding: 40px 0;
}
.skin-tint-section .top-heading {
  font-size: 28px;
  font-weight: 600;
  margin-bottom: 10px;
}
.skin-tint-section .sub-heading {
  font-size: 18px;
  color: #666;
  margin-bottom: 40px;
}
.skin-tint-columns {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 20px;
align-items: center;
}
.skin-tint-col {
  flex: 1;
  min-width: 280px;
  background: white;
  border-radius: 16px;
  padding: 0
  text-align: center;
}
.skin-tint-stat {
  font-size: 32px;
  font-weight: bold;
  color: #12372A;
  margin-bottom: 10px;
}
.skin-tint-title, 
  .skin-tint-title1,
  .skin-tint-title2{
  font-weight: bold;
  margin-bottom:0;
  color: #12372A;
  font-size: 19px;
  line-height: 18px;
}
.skin-tint-text,
  .skin-tint-text1{
  font-size: 16px;
  color: #000;
}
.before-after-container {
  position: relative;
  overflow: hidden;
  border-radius: 16px;
  aspect-ratio: 3/4;
  border: 3px solid #12372A;
}
.before-after-container img {
  position: absolute;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.before-img {
  z-index: 1;
  clip-path: inset(0 50% 0 0);
}
.after-img {
  z-index: 2;
  clip-path: inset(0 0 0 50%);
}
.before-after-container img {
  position: absolute;
  top: 0;
  left: 0;
  object-fit: cover;
}
.before-after-container {
  position: relative;
  overflow: hidden;
  border-radius: 16px;
  aspect-ratio: 3/4;
}
.before-after-container {
  position: relative;
  overflow: hidden;
      border-radius: 50%;
    aspect-ratio: 4 / 4
}

.before-after-container img {
  position: absolute;
  top: 0;
  left: 0;
  object-fit: cover;
  width: 100%;
  height: 100%;
}

.before-img {
  z-index: 1;
  clip-path: inset(0 50% 0 0);
  transition: clip-path 0.3s ease;
}
.after-img {
  z-index: 2;
  clip-path: inset(0 0 0 50%);
  transition: clip-path 0.3s ease;
}


.slider-handle {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 4;
  background: #ffffff00;
  border: 2px solid #ffffff;
  border-radius: 50%;
  padding: 3px 10px;
  font-size: 18px;
  cursor: ew-resize;
  user-select: none;
  z-index: 3;
  color: #fff;
  font-weight: bold;
}
.image-divider {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 2px;
  background-color: #fff;
  z-index: 999;
  left: 50%;
  transform: translateX(-50%);
  pointer-events: none;
  display: block !important;}

.before-label,
.after-label {
  position: absolute;
  bottom: 10px;
  background:  #12372A;;
  color: #FFF;
  padding: 2px 8px;
  font-size: 12px;
  font-weight: bold;
  z-index: 4;
  border-radius:50%;
}
.before-label {
  left: 10px;
}
.after-label {
  right: 10px;
}
.skin-col-left,
 .skin-col-right,
  skin-col-left1,
  skin-col-right1{
  padding: 20px;
   max-height: 400px;
}
.col-left,
 .col-right
 {
    width: 25%;
}

@media screen and (max-width: 768px) {
  .skin-tint-columns {
    flex-direction: column;
    align-items: center;
  }
  .skin-tint-before-after {
    order: 1;
  }

.col-left,
 .col-right
 {
    width: 100%;
}
}

</style>
<script>
  document.addEventListener("DOMContentLoaded", function () {
    const container = document.getElementById("beforeAfterSlider");
    const beforeImg = container.querySelector(".before-img");
    const afterImg = container.querySelector(".after-img");
    const handle = document.getElementById("sliderHandle");

    const updateClip = (x) => {
      const rect = container.getBoundingClientRect();
      const offset = Math.max(0, Math.min(x - rect.left, rect.width));
      const percent = (offset / rect.width) * 100;
      beforeImg.style.clipPath = `inset(0 ${100 - percent}% 0 0)`;
      afterImg.style.clipPath = `inset(0 0 0 ${percent}%)`;
      handle.style.left = `${percent}%`;
      container.querySelector(".image-divider").style.left = `${percent}%`;
    };

    let dragging = false;

    handle.addEventListener("mousedown", () => (dragging = true));
    window.addEventListener("mouseup", () => (dragging = false));
    window.addEventListener("mousemove", (e) => {
      if (dragging) updateClip(e.clientX);
    });

    handle.addEventListener("touchstart", () => (dragging = true));
    window.addEventListener("touchend", () => (dragging = false));
    window.addEventListener("touchmove", (e) => {
      if (dragging) updateClip(e.touches[0].clientX);
    });
  });
</script>

<div class="skin-tint-section">
<div class="page-width">
  <h2 class="top-heading">{{ section.settings.top_heading }}</h2>
  <p class="sub-heading">{{ section.settings.sub_heading }}</p>
  <div class="skin-tint-columns">
    
    <!-- Left Column -->
    <div class="col-left">
    <div class="skin-tint-col skin-col-left">
      {% if section.settings.left_image %}
        <img src="{{ section.settings.left_image | img_url: 'medium' }}" alt="Left stat image" style="max-width: 60px; margin: 0 auto 5px;">
      {% endif %}
      <div class="skin-tint-stat">{{ section.settings.left_stat }}</div>
      <div class="skin-tint-title">{{ section.settings.left_title }}</div>
      <p class="skin-tint-text">{{ section.settings.left_text }}</p>
    </div>
   <div class="skin-tint-col skin-col-left1">
      {% if section.settings.left_image1 %}
        <img src="{{ section.settings.left_image1 | img_url: 'medium' }}" alt="Left stat image" style="max-width: 60px; margin: 0 auto 5px;">
      {% endif %}
      <div class="skin-tint-stat1">{{ section.settings.left_stat1 }}</div>
      <div class="skin-tint-title1">{{ section.settings.left_title1 }}</div>
      <p class="skin-tint-text1">{{ section.settings.left_text1 }}</p>
    </div>
    </div>
<!-- Center Column -->
<div class="skin-tint-col skin-tint-before-after">
  <div class="before-after-container" id="beforeAfterSlider">
    {% if section.settings.before_image %}
      <img src="{{ section.settings.before_image | img_url: 'master' }}" alt="Before" class="before-img">
    {% endif %}
    {% if section.settings.after_image %}
      <img src="{{ section.settings.after_image | img_url: 'master' }}" alt="After" class="after-img">
    {% endif %}
    <div class="image-divider"></div>
    <div class="slider-handle" id="sliderHandle">&#x21c4;</div>
    <div class="before-label">{{ section.settings.before_label }}</div>
    <div class="after-label">{{ section.settings.after_label }}</div>
  </div>
</div>


    <!-- Right Column -->
    <div class="col-right">
    <div class="skin-tint-col skin-col-right">
      {% if section.settings.right_image1 %}
        <img src="{{ section.settings.right_image1 | img_url: 'medium' }}" alt="Right stat image" style="max-width: 60px; margin: 0 auto 5px;">
      {% endif %}
      <div class="skin-tint-stat">{{ section.settings.right_stat }}</div>
      <div class="skin-tint-title">{{ section.settings.right_title }}</div>
      <p class="skin-tint-text">{{ section.settings.right_text }}</p>
    </div>
     <div class="skin-tint-col skin-col-right1">
      {% if section.settings.right_image %}
        <img src="{{ section.settings.right_image | img_url: 'medium' }}" alt="Right stat image" style="max-width: 60px; margin: 0 auto 5px;">
      {% endif %}
      <div class="skin-tint-stat1">{{ section.settings.right_stat1 }}</div>
      <div class="skin-tint-title1">{{ section.settings.right_title1 }}</div>
      <p class="skin-tint-text1">{{ section.settings.right_text1 }}</p>
    </div>
    </div>
  </div>
</div>
</div>
{% schema %}
{
  "name": "Skin Tint Feature Section",
  "settings": [
    {
      "type": "text",
      "id": "top_heading",
      "label": "Top Heading",
      "default": "This Is NOT Just Another Skin Tint"
    },
    {
      "type": "text",
      "id": "sub_heading",
      "label": "Subheading",
      "default": "It’s the skincare-infused beauty balm that gives you flawless, second-skin coverage in one effortless swipe."
    },
    {
      "type": "image_picker",
      "id": "left_image",
      "label": "Left Column Image"
    },
    {
      "type": "text",
      "id": "left_stat",
      "label": "Left Column Stat",
      "default": "94%"
    },
    {
      "type": "text",
      "id": "left_title",
      "label": "Left Column Heading",
      "default": "INSTANT COVERAGE"
    },
    {
      "type": "textarea",
      "id": "left_text",
      "label": "Left Column Text",
      "default": "94% of women agreed it instantly blurred dark spots and hyperpigmentation, creating a more even skin tone."
    },
    {
  "type": "image_picker",
  "id": "left_image1",
  "label": "Left Column Image 2"
},
{
  "type": "text",
  "id": "left_stat1",
  "label": "Left Column Stat 2",
  "default": "92%"
},
{
  "type": "text",
  "id": "left_title1",
  "label": "Left Column Heading 2",
  "default": "SKINCARE POWER"
},
{
  "type": "textarea",
  "id": "left_text1",
  "label": "Left Column Text 2",
  "default": "Formulated with niacinamide and SPF to help even skin tone and protect from sun damage."
},
    {
      "type": "image_picker",
      "id": "before_image",
      "label": "Before Image"
    },
    {
      "type": "image_picker",
      "id": "after_image",
      "label": "After Image"
    },
    {
  "type": "text",
  "id": "before_label",
  "label": "Before Label",
  "default": "BEFORE"
},
{
  "type": "text",
  "id": "after_label",
  "label": "After Label",
  "default": "AFTER"
}
,
    {
      "type": "image_picker",
      "id": "right_image",
      "label": "Right Column Image"
    },
    {
      "type": "text",
      "id": "right_stat",
      "label": "Right Column Stat",
      "default": "Lorem Ipsum"
    },
    {
      "type": "text",
      "id": "right_title",
      "label": "Right Column Heading",
      "default": "SECOND-SKIN FEEL"
    },
    {
      "type": "textarea",
      "id": "right_text",
      "label": "Right Column Text",
      "default": "Lorem Ipsum"
    },{
  "type": "image_picker",
  "id": "right_image1",
  "label": "Right Column Image 2"
},
{
  "type": "text",
  "id": "right_stat1",
  "label": "Right Column Stat 2",
  "default": "91%"
},
{
  "type": "text",
  "id": "right_title1",
  "label": "Right Column Heading 2",
  "default": "LASTING WEAR"
},
{
  "type": "textarea",
  "id": "right_text1",
  "label": "Right Column Text 2",
  "default": "91% of women said it stayed in place and felt weightless all day."
}
  ],
  "presets": [
    {
      "name": "before-after",
      "category": "Image"
    }
  ]
}
{% endschema %}
