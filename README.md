<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Digital Health Center page 1</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-4bw+/aepP/YC94hEpVNVgiZdgIC5+VKNBQNGCHeKRQN+PtmoHDEXuppvnDJzQIu9" crossorigin="anonymous">
  </head>
  

  <style>
    body {
            background-image: url("/static/bg1.jpg");
            background-size: cover;
            background-repeat: no-repeat;
            background-attachment: fixed;
        }

        .logo {
            width: 50px;
            height: 50px;
            color: rgba(11, 169, 146, .5);
            margin-top: 0;
            margin-left: 2px;
        }

        .myimg {
            width: 50px;
            height: 50px;
            border: 2px solid black;
            border-radius: 25px;
        }
        .container {
            background: rgba(11, 169, 146, .5);
            color: white;
            border-radius: 15px;
            padding: 40px;
        }
        .main-heading {
          text-align: center;
          margin-bottom: 40px;
          animation: fadeInUp 1s ease-in-out;
        }
        
        .digital-text {
          font-size: 3rem;
          font-weight: 700;
          background: linear-gradient(90deg, rgba(230,19,202,1) 0%, rgba(0,255,200,1) 100%);
          -webkit-background-clip: text;
          -webkit-text-fill-color: transparent;
          text-transform: uppercase;
          letter-spacing: 2px;
          margin-bottom: 10px;
        }
        
        .health-text {
          font-size: 2.5rem;
          color: #333;
          font-weight: 600;
          letter-spacing: 1px;
        }
        .error-message {
          color: red;
          font-size: 18px;
          font-weight: bold;
          margin-top: 10px;
          text-align: center;
        }
        
        


        




    </style>
</head>
<body>
   

<!-- Navbar -->
<nav class="navbar navbar-expand-lg navbar-dark bg-secondary fixed-top"> 
  <div class="container-fluid" >
      <!-- Logo at the top-left corner -->
      <div class="logo">
          <img class="myimg" src="{{ url_for('static', filename='l1.avif') }}" alt="">
      </div>

      <a class="navbar-brand" href="#">Health Center</a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent" >
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
              <li class="nav-item">
                  <a class="nav-link active" aria-current="page" href="#">Home</a>
              </li>
              <li class="nav-item">
                  <a class="nav-link" href="/about">About</a>
              </li>
              <li class="nav-item">
                  <a class="nav-link" href="/contact">Contact</a>
              </li>
              <li class="nav-item">
                  <a class="nav-link" href="/developer">Developer</a>
              </li>
              <li class="nav-item">
                  <a class="nav-link" href="/blog">Blog</a>
              </li>
          </ul>
      </div>
  </div>
</nav>

  



    


    <!-- Main Content -->
    <div style="flex: 1; display: flex; flex-direction: column; justify-content: center; align-items: center; padding-top: 60px; transform: translateY(20px);">
      <div class="main-heading">
        <h1 class="digital-text">DIGITAL</h1>
        <h1 class="health-text">Health Center</h1>
      </div>
      
        <div class="container my-4 mt-4" style="background: rgba(138, 244, 237, 0.5); color: rgb(3, 3, 3); border-radius: 100px; padding: 100px; max-width: 700px; margin-left: auto; margin-right: 50px; top-down : 120px;">
            <form action="/predict" method="post">
                <div class="form-group">
                    <label for="symptoms">Select Symptoms:</label>
                    <input type="text" class="form-control" id="symptoms" name="symptoms" placeholder="Type Symptoms such as itching, sleeping, aching etc." value="{{ request.form.get('symptoms', '') }}">
                    {% if message %}
  <div class="error-message">{{ message }}</div>
{% endif %}

                </div>
                
                <br>
                <button type="button" id="startSpeechRecognition" class="btn btn-primary" style="margin-left:3px; border:1px solid white; border-radius:40px; color: white; background:black">
                    Start Speech Recognition
                </button>
                <script>
                  document.getElementById('startSpeechRecognition').addEventListener('click', function () {
                    if ('webkitSpeechRecognition' in window) {
                      const recognition = new webkitSpeechRecognition();
                      recognition.lang = 'en-US';
                      recognition.interimResults = false;
                      recognition.maxAlternatives = 1;
                
                      recognition.start();
                
                      recognition.onresult = function (event) {
                        const transcript = event.results[0][0].transcript;
                        document.getElementById('symptoms').value = transcript;
                      };
                
                      recognition.onerror = function (event) {
                        alert('Error occurred in recognition: ' + event.error);
                      };
                    } else {
                      alert('Speech recognition not supported in this browser.');
                    }
                  });
                </script>
                <br>

                
                <br>
                <button type="submit" class="btn btn-danger btn-lg" style="width: 100%; padding: 6px; margin-bottom: 5px; background: rgba(11, 17, 17, 0.92); color: rgb(249, 248, 248);">Predict</button>
            </form>
        </div>
    </div>
    
  
  
  

</body>







{% if predicted_disease %}
<!-- Result Section -->
<div id="resultContainer" class="slide-from-button" style="position: absolute; right: 20px;  width: 700px; background:rgb(184, 208, 231); border-radius: 16px; padding: 20px; box-shadow: 0 8px 20px rgba(0,0,0,0.1);">

    <h3 class="text-left mb-3" style="color: black;">Result Of Our AI System</h3>
    <center>

    <div class="result-container">
      <!-- Buttons to toggle display -->
      <button class="toggle-button" data-bs-toggle="modal" data-bs-target="#diseaseModal" style="padding:4px;  margin: 5px 40px 5px 0; font-size:20px;font-weight:bold; width:140px; border-radius:5px; background:#99F741;color:black;">Disease</button>
      <button class="toggle-button" data-bs-toggle="modal" data-bs-target="#descriptionModal" style="padding:4px; margin: 5px 40px 5px 0; font-size:20px;font-weight:bold; width:140px; border-radius:5px; background:hsl(288, 94%, 49%) ;color:black;">Description</button>
      <button class="toggle-button" data-bs-toggle="modal" data-bs-target="#precautionModal" style="padding:4px; margin: 5px 40px 5px 0; font-size:20px;font-weight:bold; width:140px; border-radius:5px; background:#11deec ;color:black;">Precaution</button>
      <button class="toggle-button" data-bs-toggle="modal" data-bs-target="#medicationsModal" style="padding:4px; margin: 5px 40px 5px 0; font-size:20px;font-weight:bold; width:140px;border-radius:5px; background:#a6011d ;color:black;">Medications</button>
      <button class="toggle-button" data-bs-toggle="modal" data-bs-target="#workoutsModal" style="padding:4px; margin: 5px 40px 5px 0; font-size:20px;font-weight:bold; width:140px; border-radius:5px; background:#0af2b0b0 ;color:black;">Workouts</button>
      <button class="toggle-button" data-bs-toggle="modal" data-bs-target="#dietsModal" style="padding:4px; margin: 5px 40px 5px 0; font-size:20px;font-weight:bold; width:140px; border-radius:5px; background:#d29f08ea;color:black;">Diets</button>
  </div>
</center>
</div>




{% endif %}

<!-- Disease Modal -->
    <div class="modal fade" id="diseaseModal" tabindex="-1" aria-labelledby="diseaseModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header" style="background-color: #020606; color:rgb(152, 226, 224);"> <!-- Set header background color inline -->
                    <h5 class="modal-title" id="diseaseModalLabel">Predicted Disease</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body" style="background-color: #76e8be;"> <!-- Set modal body background color inline -->
                    <p>{{ predicted_disease }}</p>
                </div>
            </div>
        </div>
    </div>


    <!-- Description Modal -->
    <div class="modal fade" id="descriptionModal" tabindex="-1" aria-labelledby="descriptionModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header" style="background-color: #020606; color:rgb(141, 159, 211);">
                    <h5 class="modal-title" id="descriptionModalLabel">Description</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body" style="background-color: #76e8be;">
                    <p>{{ dis_des }}</p>
                </div>
            </div>
        </div>
    </div>

<!-- Precaution Modal -->
    <div class="modal fade" id="precautionModal" tabindex="-1" aria-labelledby="precautionModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header" style="background-color: #020606; color:white;">
                    <h5 class="modal-title" id="precautionModalLabel">Precaution</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body" style="background-color: #76e8be;">
                    <ul>
                        {% for i in my_precautions %}
                            <li>{{ i }}</li>
                        {% endfor %}
                    </ul>
                </div>
            </div>
        </div>
    </div>




    <!-- Medications Modal -->
    <div class="modal fade" id="medicationsModal" tabindex="-1" aria-labelledby="medicationsModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header" style="background-color: #020606; color:white;">
                    <h5 class="modal-title" id="medicationsModalLabel">Medications</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body" style="background-color: #76e8be;">
                    <ul>
                        {% for i in medications %}
                            <li>{{ i }}</li>
                        {% endfor %}
                    </ul>
                </div>
            </div>
        </div>
    </div>

    <!-- Workouts Modal -->
    <div class="modal fade" id="workoutsModal" tabindex="-1" aria-labelledby="workoutsModalLabel" aria-hidden="true">
        <div class="modal-dialog" >
            <div class="modal-content">
                <div class="modal-header" style="background-color: #020606; color:white;">
                    <h5 class="modal-title" id="workoutsModalLabel">Workouts</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body" style="background-color: #76e8be;">
                    <ul>
                        {% for i in workout %}
                            <li>{{ i }}</li>
                        {% endfor %}
                    </ul>
                </div>
            </div>
        </div>
    </div>

    <!-- Diets Modal -->
    <div class="modal fade" id="dietsModal" tabindex="-1" aria-labelledby="dietsModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header" style="background-color: #020606; color:white;">
                    <h5 class="modal-title" id="dietsModalLabel">Diets</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body" style="background-color: #76e8be;">
                    <ul>
                        {% for i in my_diet %}
                            <li>{{ i }}</li>
                        {% endfor %}
                    </ul>
                </div>
            </div>
        </div>
    </div>




  



    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.1/dist/js/bootstrap.bundle.min.js" integrity="sha384-HwwvtgBNo3bZJJLYd8oVXjrBZt8cqVSpeBNS5n7C8IVInixGAoxmnlMuBnhbgrkm" crossorigin="anonymous"></script>
</body>

</html>




<pre>

   






</pre>



<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Medicine Recommendation Chatbot</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      font-family: Arial, sans-serif;
      
    }

    #chatContainer {
      position: fixed;
      bottom: 100px;
      right: 20px;
      width: 500px;
      background: rgb(90, 196, 198);
      border: 1px solid #ccc;
      border-radius: 10px;
      padding: 10px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }

    #chatbox {
      height: 200px;
      overflow-y: auto;
      border: 1px solid #ccc;
      padding: 5px;
      margin-bottom: 10px;
      border-radius: 5px;
      background-image: url('{{ url_for("static", filename="c5.jpg") }}'); /* Update the path to your image */
      
      font-size: 14px;
    }

    input[type="text"] {
      width: calc(100% - 60px);
      padding: 5px;
      border-radius: 5px;
      border: 1px solid #ccc;
      

      
    }

    button {
      padding: 5px 10px;
      margin-left: 5px;
      border: none;
      background:rgb(247, 8, 8);
      color: white;
      border-radius: 5px;
      cursor: pointer;
    }

    


    .chatbot-icon-container {
      position: fixed;
      right: 20px;
      bottom: 20px;
      width: 80px;
      height: 80px;
      display: flex;
      align-items: center;
      justify-content: center;
      z-index: 1000;
      border radius:20px;
      border color:black;
    }
   
    
    
  </style>
</head>
<body>

  <!-- Chatbot Icon -->
  <div class="chatbot-icon-container">
     <span class="glow-layer1"></span>
    <span class="glow-layer2"></span>
    <img
      src="https://cdn-icons-png.flaticon.com/512/4712/4712109.png"
      alt="Robot Icon"
      width="50"
      height="50"
      onclick="toggleChatbot()"
      style="cursor: pointer;"
    />
   
    
  </div>
  


  <!-- Chat Container -->
  <div id="chatContainer" style="display: none;">
    <h3>Medicine Chatbot</h3>
    <div id="chatbox"></div>
    <input type="text" id="userInput" placeholder="Enter your symptoms..." />
    <button onclick="sendMessage()">Send</button>
  </div>

  <script>
    const input = document.getElementById("userInput");
const chatbox = document.getElementById("chatbox");
const chatContainer = document.getElementById("chatContainer");

function toggleChatbot() {
  chatContainer.style.display = chatContainer.style.display === "none" ? "block" : "none";
}

input.addEventListener("keydown", function (event) {
  if (event.key === "Enter") {
    event.preventDefault();
    sendMessage();
  }
});

const recommendations = {
  "fever": ["Paracetamol", "Ibuprofen", "Stay hydrated"],
  "headache": ["Aspirin", "Ibuprofen", "Rest in a dark room"],
  "cold": ["Antihistamines", "Decongestants", "Drink warm fluids"],
  "cough": ["Cough syrup", "Honey tea", "Stay hydrated"],
  "stomach pain": ["Antacids", "Buscopan", "BRAT diet (Banana, Rice, Applesauce, Toast)"],
  "body ache": ["Ibuprofen", "Pain relief balm", "Warm compress"],
  "sore throat": ["Lozenges", "Salt water gargle", "Warm teas"],
  "itching": ["Antihistamine cream", "Calamine lotion", "Avoid scratching"],
  "back pain": ["Muscle relaxants", "Physical therapy", "Heat therapy"],
  "dizziness": ["Hydration", "Rest", "Monitor symptoms"],
  "nausea": ["Antiemetic", "Ginger tea", "Light meals"],
  "vomiting": ["Oral rehydration", "Antiemetic", "Rest"],
  "diarrhea": ["ORS", "Probiotics", "BRAT diet"],
  "constipation": ["Fiber supplements", "Laxatives", "Hydration"],
  "allergies": ["Antihistamines", "Nasal spray", "Avoid allergens"],
  "rash": ["Topical cream", "Antihistamines", "Keep area clean"],
  "joint pain": ["NSAIDs", "Physical therapy", "Rest"],
  "muscle pain": ["Ibuprofen", "Massage", "Warm compress"],
  "earache": ["Pain reliever", "Warm compress", "Consult doctor"],
  "toothache": ["Ibuprofen", "Clove oil", "Dental visit"],
  "sinusitis": ["Decongestants", "Nasal saline", "Steam inhalation"],
  "bronchitis": ["Cough suppressant", "Expectorant", "Rest"],
  "asthma": ["Inhalers", "Bronchodilators", "Avoid triggers"],
  "anxiety": ["Therapy", "Anti-anxiety medication", "Relaxation techniques"],
  "depression": ["Antidepressants", "Counseling", "Lifestyle changes"],
  "insomnia": ["Melatonin", "Sleep hygiene", "Relaxation techniques"],
  "hypertension": ["ACE inhibitors", "Beta blockers", "Lifestyle modifications"],
  "diabetes": ["Insulin", "Metformin", "Dietary changes"],
  "acne": ["Topical benzoyl peroxide", "Salicylic acid", "Consult dermatologist"],
  "eczema": ["Moisturizers", "Topical steroids", "Avoid irritants"],
  "psoriasis": ["Topical treatments", "Phototherapy", "Systemic medications"],
  "migraine": ["Triptans", "NSAIDs", "Rest in dark room"],
  "vertigo": ["Meclizine", "Balance therapy", "Hydration"],
  "chest pain": ["Nitroglycerin", "Aspirin", "Emergency care"],
  "palpitations": ["Beta blockers", "Lifestyle changes", "Stress management"],
  "heartburn": ["Antacids", "H2 blockers", "Avoid trigger foods"],
  "indigestion": ["Antacids", "Digestive enzymes", "Eat slowly"],
  "gastritis": ["Antacids", "Proton pump inhibitors", "Avoid spicy foods"],
  "ulcers": ["Antibiotics", "Proton pump inhibitors", "Avoid NSAIDs"],
  "anemia": ["Iron supplements", "Vitamin B12", "Dietary changes"],
  "hypothyroidism": ["Thyroid hormone replacement", "Regular monitoring", "Consult endocrinologist"],
  "hyperthyroidism": ["Beta blockers", "Antithyroid medications", "Radioactive iodine"],
  "arthritis": ["NSAIDs", "Physical therapy", "Weight management"],
  "sprain": ["Rest", "Ice", "Compression and elevation"],
  "strain": ["Rest", "Ice", "Gentle stretching"],
  "conjunctivitis": ["Antibiotic eye drops", "Cold compress", "Maintain hygiene"],
  "eye irritation": ["Artificial tears", "Rest", "Cool compress"],
  "blurred vision": ["Corrective lenses", "Rest", "Eye exam"],
  "ear infection": ["Antibiotics", "Pain relievers", "Warm compress"],
  "fibromyalgia": ["Pain relievers", "Exercise", "Stress management"],
  "leg cramps": ["Hydration", "Magnesium supplements", "Stretching exercises"],
  "swollen ankles": ["Elevation", "Compression stockings", "Reduce salt intake"],
  "edema": ["Diuretics", "Reduce salt intake", "Monitor fluid levels"],
  "urinary tract infection": ["Antibiotics", "Increased water intake", "Pain relievers"],
  "kidney stones": ["Pain relievers", "Hydration", "Medical evaluation"],
  "bladder infection": ["Antibiotics", "Increased water intake", "Urinary alkalizers"],
  "prostate issues": ["Alpha blockers", "5-alpha-reductase inhibitors", "Consult urologist"],
  "menstrual cramps": ["NSAIDs", "Heat therapy", "Rest"],
  "irregular periods": ["Hormonal therapy", "Dietary changes", "Consult gynecologist"],
  "hot flashes": ["Hormone therapy", "Lifestyle changes", "Cooling techniques"],
  "osteoporosis": ["Calcium supplements", "Vitamin D", "Bisphosphonates"],
  "dandruff": ["Anti-dandruff shampoo", "Scalp massage", "Tea tree oil"],
  "hair loss": ["Minoxidil", "Nutritional supplements", "Consult dermatologist"],
  "nail fungus": ["Antifungal creams", "Oral antifungals", "Keep nails dry"],
  "skin infection": ["Antibiotic ointment", "Oral antibiotics", "Keep area clean"],
  "boils": ["Warm compress", "Topical antibiotics", "Maintain hygiene"],
  "cellulitis": ["Oral antibiotics", "Elevation", "Rest"],
  "wound care": ["Clean the wound", "Antibiotic ointment", "Cover with bandage"],
  "sunburn": ["Aloe vera", "Cool compress", "Moisturizers"],
  "poison ivy": ["Topical steroids", "Oatmeal baths", "Avoid scratching"],
  "insect bites": ["Antihistamines", "Topical cream", "Cold compress"],
  "stye": ["Warm compress", "Antibiotic ointment", "Maintain eye hygiene"],
  "hemorrhoids": ["Topical creams", "Fiber supplements", "Sitz baths"],
  "varicose veins": ["Compression stockings", "Exercise", "Elevation"],
  "peripheral neuropathy": ["Pain relievers", "Physical therapy", "Vitamin supplements"],
  "tingling": ["Check vitamin levels", "Rest", "Consult doctor"],
  "numbness": ["Medical evaluation", "Physical therapy", "Nutritional support"],
  "panic attack": ["Breathing techniques", "Reassurance", "Consult professional"],
  "phobia": ["Exposure therapy", "Counseling", "Relaxation techniques"],
  "PTSD": ["Therapy", "Medication", "Support groups"],
  "obesity": ["Dietary changes", "Exercise", "Behavioral therapy"],
  "weight loss": ["Balanced diet", "Regular exercise", "Lifestyle modifications"],
  "scoliosis": ["Physical therapy", "Bracing", "Surgical consultation"],
  "kyphosis": ["Physical therapy", "Pain management", "Posture correction"],
  "lactose intolerance": ["Lactase supplements", "Dairy alternatives", "Dietary adjustments"],
  "gluten intolerance": ["Gluten-free diet", "Nutritional counseling", "Avoid cross-contamination"],
  "irritable bowel syndrome": ["Dietary fiber", "Probiotics", "Stress management"],
  "acid reflux": ["Antacids", "H2 blockers", "Avoid trigger foods"],
  "GERD": ["Proton pump inhibitors", "Lifestyle changes", "Dietary modifications"],
  "cholecystitis": ["Antibiotics", "Pain management", "Surgical consultation"],
  "hepatitis": ["Antiviral medication", "Rest", "Regular monitoring"],
  "cirrhosis": ["Avoid alcohol", "Nutritional support", "Liver transplant evaluation"],
  "pancreatitis": ["Hospitalization", "IV fluids", "Pain management"],
  "gout": ["NSAIDs", "Colchicine", "Lifestyle modifications"],
  "narcolepsy": ["Stimulants", "Scheduled naps", "Sleep hygiene"],
  "snoring": ["Lifestyle changes", "CPAP machine", "Consult sleep specialist"],
  "sleep apnea": ["CPAP machine", "Weight loss", "Sleep study"],
  "skin rash": ["Topical steroids", "Antihistamines", "Avoid irritants"],
  "inflammation": ["NSAIDs", "Cold compress", "Rest"],
  "joint stiffness": [
    "Warm-up exercises", 
    "Physical therapy", 
    "Pain relievers"
  ]
};

function appendMessage(sender, message) {
  const messageElement = document.createElement("div");
  messageElement.textContent = `${sender}: ${message}`;
  chatbox.appendChild(messageElement);
  chatbox.scrollTop = chatbox.scrollHeight;
}

function sendMessage() {
  const userInput = input.value.trim().toLowerCase();
  if (userInput === "") return;

  appendMessage("You", input.value);
  input.value = "";

  let response = "I'm sorry, I don't have information on that. Can you try describing your symptoms again?";

  // Greeting detection
  const greetings = ["hi","hii","hiii","hiiii", "hello", "hey", "good morning", "good evening"];
  if (greetings.includes(userInput)) {
    response = "Hello! How can I assist you today?";
  }else if (userInput.includes("how are you")) {
    response = "I'm here and ready to help! How can I assist you today?";
  }
  else {
    // Check symptoms in recommendations
    for (const symptom in recommendations) {
      if (userInput.includes(symptom)) {
        response = `For ${symptom}, I recommend: ${recommendations[symptom].join(", ")}.`;
        break;
      }
    }
  }

  setTimeout(() => appendMessage("Bot", response), 500); // Slight delay for natural feel
}

  </script>
  
</body>
</html>







 <h1> 












 </h1>



 <!doctype html>
 <html lang="en">
   <head>
     <meta charset="utf-8">
     <meta name="viewport" content="width=device-width, initial-scale=1">
     <title>Digital Health Center Page 1</title>
     <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-4bw+/aepP/YC94hEpVNVgiZdgIC5+VKNBQNGCHeKRQN+PtmoHDEXuppvnDJzQIu9" crossorigin="anonymous">
     <style>
       body {
         margin: 0;
         padding: 0;
         font-family: Arial, sans-serif;
       }
 
       .page1-container {
         background-image: url("/static/beu3.avif");
         background-size: cover;
         background-repeat: no-repeat;
         background-attachment: fixed;
         min-height: 100vh;
       }
 
       .goal-img {
         max-width: 400px;
         width: 100%;
         height: auto;
         border-radius: 12px;
         box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
         transition: transform 0.3s ease, box-shadow 0.3s ease;
       }
 
       .goal-img:hover {
         transform: scale(1.05);
         box-shadow: 0 6px 18px rgba(0, 0, 0, 0.2);
       }
 
       .symptom-section {
         max-width: 1100px;
         margin: 0 auto;
       }
 
       .symptom-box {
         background: rgba(138, 244, 237, 0.5);
         border-radius: 60px;
         color: #333;
         box-shadow: 0 8px 16px rgba(0, 0, 0, 0.1);
       }
 
       .symptom-box ul li {
         margin-bottom: 10px;
       }
 
       .symptom-img {
         max-width: 300px;
         width: 100%;
         height: auto;
         border-radius: 12px;
         transition: transform 0.3s ease, box-shadow 0.3s ease;
         box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
       }
 
       .symptom-img:hover {
         transform: scale(1.05);
         box-shadow: 0 6px 18px rgba(0, 0, 0, 0.2);
       }
 
       .image-gallery .image-card {
         max-width: 300px;
         transition: transform 0.3s ease, box-shadow 0.3s ease;
         border-radius: 10px;
         overflow: hidden;
       }
 
       .image-gallery .image-card:hover {
         transform: scale(1.05);
         box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
       }
 
       .image-gallery img {
         width: 100%;
         height: auto;
         display: block;
         border-radius: 10px;
       }
     </style>
   </head>
   
 
   <body>
     <div class="page1-container">
       <div style="background: #0ba992; color: black; text-align: center; padding: 20px;">
         <h1>We Are Always Ready to Help You & Your Family</h1>
       </div>
 
       <div style="padding: 20px; display: flex; justify-content: space-between; align-items: flex-start;">
         <div class="container" style="background: rgba(138, 244, 237, 0.5); color: rgb(223, 207, 212); border-radius: 100px; padding: 100px; max-width: 1000px; margin-left: 50px;">
           <h1 style="color: black;">Instant and Reliable Medicine Recommendations</h1>
           <p style="font-size: 18px; color: black;">
             Our Medicine Recommendation System is designed to provide you with quick and reliable suggestions based on your symptoms.
           </p>
           <p style="font-size: 18px; color: black;">
             It ensures that you get safe and effective recommendations instantly, making self-care easier and more accessible anytime, anywhere.
           </p>
         </div>
         <div style="flex-shrink: 0; margin-left: 20px;">
           <img class="goal-img" src="{{ url_for('static', filename='b5.avif') }}" alt="Health Image">
         </div>
       </div>
     </div>
 
     <div style="max-width: 1500px; margin: 40px auto; padding: 40px; background-color: rgb(146, 206, 214); border-radius: 12px; box-shadow: 0 4px 12px rgba(0,0,0,0.1); text-align: center;">
       <h1 style="color: black; padding: 20px;">How It Works</h1>
       <p style="font-size: 18px; color: black; margin-bottom: 40px;">
         Simply enter your symptoms into the chatbot, and our system will analyze your input to provide the best recommendations.
       </p>
       <div style="display: flex; justify-content: center; align-items: center; gap: 30px; flex-wrap: wrap;">
         <img class="goal-img" src="{{ url_for('static', filename='b6.avif') }}" alt="Medical">
         <img class="goal-img" src="{{ url_for('static', filename='b7.avif') }}" alt="Medical">
         <img class="goal-img" src="{{ url_for('static', filename='b8.avif') }}" alt="Medical">
       </div>
     </div>
 
     <div class="container symptom-section my-5">
       <div class="symptom-box p-5 rounded-5">
         <h2 class="mb-4 text-center fw-bold text-dark">Common Symptoms and Recommendations</h2>
         <ul class="list-unstyled fs-5">
           <li><strong>Fever:</strong> Paracetamol, Ibuprofen, stay hydrated</li>
           <li><strong>Headache:</strong> Aspirin, Ibuprofen, rest in a dark room</li>
           <li><strong>Cold:</strong> Antihistamines, decongestants, drink warm fluids</li>
           <li><strong>Cough:</strong> Cough syrup, honey tea, stay hydrated</li>
           <li><strong>Stomach Pain:</strong> Antacids, BRAT diet (Bananas, Rice, Applesauce, Toast)</li>
         </ul>
         <div class="image-row d-flex justify-content-center align-items-center gap-4 flex-wrap mt-5">
           <img src="{{ url_for('static', filename='m1.jpg') }}" alt="Medicine1" class="symptom-img">
           <img src="{{ url_for('static', filename='m2.jpg') }}" alt="Medicine2" class="symptom-img">
           <img src="{{ url_for('static', filename='m3.jpg') }}" alt="Medicine3" class="symptom-img">
         </div>
       </div>
     </div>
 
     <h2 style="text-align: center; font-size: 2.5rem; color: black; margin-top: 40px; margin-bottom: 20px;">Our Goal</h2>
     <p style="max-width: 800px; margin: 0 auto 40px auto; font-size: 1.2rem; line-height: 1.6; color: #34495e; text-align: center;">
       We aim to empower individuals to take control of their health by providing accessible, reliable, and evidence-based medical recommendations.
     </p>
     <div style="display: flex; justify-content: center; align-items: center; gap: 30px; flex-wrap: wrap; padding-bottom: 50px;">
       <img class="goal-img" src="{{ url_for('static', filename='oo1.png') }}" alt="goal1">
       <img class="goal-img" src="{{ url_for('static', filename='o2.avif') }}" alt="goal2">
     </div>
 
     <section class="info-section py-5 text-center text-white" style="background-color: #0ba992;">
       <div class="container">
         <h2 class="mb-3 fw-bold">Stay Healthy with Smart AI Support</h2>
         <p class="lead mb-4">
           Using Machine Learning and Natural Language Processing, our chatbot offers 24/7 trusted guidance on symptoms, medications, and wellness tips — all at your fingertips.
         </p>
         <div class="image-gallery d-flex flex-wrap justify-content-center gap-4 mt-4">
           <div class="image-card">
             <img src="{{ url_for('static', filename='h1.png') }}" alt="Medicine 1" class="img-fluid">
           </div>
           <div class="image-card">
             <img src="{{ url_for('static', filename='h2.jpg') }}" alt="Medicine 2" class="img-fluid">
           </div>
           <div class="image-card">
             <img src="{{ url_for('static', filename='h3.webp') }}" alt="Medicine 3" class="img-fluid">
           </div>
         </div>
       </div>
     </section>
 
     <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.1/dist/js/bootstrap.bundle.min.js" integrity="sha384-HoA0EmKZjg3kW9S54wNG0Ax7Anxr1j403rwhhtjfiPgk41IrTnfjpJ1rssZCvGSy" crossorigin="anonymous"></script>
   </body>
 </html>
 



  
  
  

 <!DOCTYPE html>
 <html lang="en">
   <head>
     <meta charset="utf-8">
     <meta name="viewport" content="width=device-width, initial-scale=1">
     <title>Digital Health Center Page 1</title>
     <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-4bw+/aepP/YC94hEpVNVgiZdgIC5+VKNBQNGCHeKRQN+PtmoHDEXuppvnDJzQIu9" crossorigin="anonymous">
 
     <style>
       body, html {
         margin: 0;
         padding: 0;
         height: 100%;
         font-family: Arial, sans-serif;
       }
 
       /* Page-specific background */
       .page1-container {
         background-image: url("/static/beu.avif");
         background-size: cover;
         background-repeat: no-repeat;
         background-attachment: fixed;
         min-height: 100vh;
         padding-top: 60px;
       }
 
       .hero-section {
         padding: 60px 0;
         position: relative;
         color: rgb(211, 18, 134);
       }
 
       .hero-section::after {
         content: "";
         position: absolute;
         top: 0; left: 0; right: 0; bottom: 0;
         background: none;
         z-index: 1;
       }
 
       .hero-content {
         position: relative;
         z-index: 2;
         color: black;
       }
 
       .feature-box {
         background: rgba(34, 40, 58, 0.9);
         border-radius: 10px;
         padding: 20px;
         box-shadow: 0 0 15px rgba(0,0,0,0.1);
         transition: transform 0.3s;
         height: 100%;
         color: white;
       }
 
       .feature-box:hover {
         transform: translateY(-5px);
       }
 
       .icon-box i {
         font-size: 40px;
         color: #2e7d32;
         margin-bottom: 15px;
       }
 
       .btn-learn-more {
         color: black;
         border-radius: 50px;
         padding: 10px 20px;
         text-decoration: none;
       }
 
       .medicine-card {
         background: rgba(255, 255, 255, 0.1);
         border-radius: 8px;
         padding: 15px;
         margin-bottom: 15px;
       }
 
       .medicine-name {
         font-weight: bold;
         color: #fff;
         font-size: 1.2rem;
       }
 
       .medicine-desc {
         font-size: 0.9rem;
       }
 
       .warning-note {
         color: #ffcc00;
         font-weight: bold;
         border-left: 3px solid #ffcc00;
         padding-left: 10px;
       }
 
       .wellness-card {
         background: rgba(74, 20, 140, 0.1);
         padding: 15px;
         border-radius: 8px;
         border-left: 4px solid #4a148c;
         margin-bottom: 15px;
       }
 
       .wellness-card h6 {
         color: #4a148c;
         font-weight: bold;
       }
 
       .wellness-card ul {
         padding-left: 20px;
         margin-bottom: 0;
       }
 
       .wellness-card li {
         margin-bottom: 5px;
       }
 
       .wellness-name {
         font-weight: bold;
         color: #2e7d32;
         font-size: 1.1rem;
         margin-bottom: 8px;
       }
     </style>
   </head>
 
   <body>
     <div class="page1-container">
       <section class="hero-section text-center text-lg-start">
         <div class="container hero-content">
           <h1 class="fw-bold">AI-Powered Medicine Recommendation</h1>
           <p class="lead">Get personalized medicine suggestions based on your symptoms and medical history</p>
 
           <div class="row align-items-center mt-5">
 
             <!-- Left Info Column -->
             <div class="col-lg-4">
               <div class="bg-primary text-white p-4 rounded">
                 <h3 class="fw-bold">Your Health, Backed by AI</h3>
                 <p>Our intelligent system reviews your symptoms and suggests suitable non-prescription medications tailored to your needs.</p>
                 <p>In case of complex or critical symptoms, we strongly recommend consulting a certified medical professional before taking any medicine.</p>
                 <div class="warning-note mt-3">
                   ⚠️ Please note: This tool is designed to assist—not replace—professional medical advice.
                 </div>
               </div>
             </div>
 
             <!-- Right Features Column -->
             <div class="col-lg-8">
               <div class="row">
                 <!-- Feature 1 -->
                 <div class="col-md-4">
                   <div class="feature-box text-center icon-box">
                     <i class="bi bi-heart-pulse"></i>
                     <h5 class="fw-bold">Head & Respiratory Wellness</h5>
                     <div class="wellness-card">
                       <div class="wellness-name">Headache Prevention</div>
                       <ul>
                         <li>Daily yoga (especially forward bends)</li>
                         <li>Proper hydration (2-3L water daily)</li>
                         <li>Neck and shoulder stretches every 2 hours</li>
                         <li>Blue light reduction for screen time</li>
                       </ul>
                     </div>
                     <div class="wellness-card">
                       <div class="wellness-name">Allergy Management</div>
                       <ul>
                         <li>Local honey consumption (1 tsp daily)</li>
                         <li>Nasal saline rinses</li>
                         <li>Morning forest walks for clean air</li>
                         <li>HEPA air filters in living spaces</li>
                       </ul>
                     </div>
                   </div>
                 </div>
 
                 <!-- Feature 2 -->
                 <div class="col-md-4">
                   <div class="feature-box text-center icon-box">
                     <i class="bi bi-brightness-high"></i>
                     <h5 class="fw-bold">Immunity Boosters</h5>
                     <div class="wellness-card">
                       <div class="wellness-name">Fever Prevention</div>
                       <ul>
                         <li>30-minute brisk walking</li>
                         <li>Vitamin D from sunlight (15 min daily)</li>
                         <li>Elderberry syrup supplementation</li>
                         <li>Warm lemon water each morning</li>
                       </ul>
                     </div>
                     <div class="wellness-card">
                       <div class="wellness-name">Respiratory Health</div>
                       <ul>
                         <li>Pranayama breathing exercises</li>
                         <li>Eucalyptus steam inhalation</li>
                         <li>High-altitude hiking for lung capacity</li>
                         <li>Humidifier use in dry climates</li>
                       </ul>
                     </div>
                   </div>
                 </div>
 
                 <!-- Feature 3 -->
                 <div class="col-md-4">
                   <div class="feature-box text-center icon-box">
                     <i class="bi bi-person-walking"></i>
                     <h5 class="fw-bold">Movement & Digestion</h5>
                     <div class="wellness-card">
                       <div class="wellness-name">Joint Mobility</div>
                       <ul>
                         <li>Swimming 3x weekly</li>
                         <li>Tai chi or qigong practice</li>
                         <li>Yoga for flexibility</li>
                         <li>Cycling on smooth terrain</li>
                       </ul>
                     </div>
                     <div class="wellness-card">
                       <div class="wellness-name">Healthy Digestion</div>
                       <ul>
                         <li>Post-meal nature walks</li>
                         <li>Stress-reducing yoga poses</li>
                         <li>Fermented foods in diet</li>
                         <li>Mindful eating practices</li>
                       </ul>
                     </div>
                   </div>
                 </div>
 
               </div>
             </div>
 
           </div>
         </div>
       </section>
     </div>
 
     <!-- Scripts -->
     <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
   </body>
 </html>
 
