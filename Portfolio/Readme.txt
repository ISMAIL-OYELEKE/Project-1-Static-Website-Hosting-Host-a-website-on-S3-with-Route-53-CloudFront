========================================================================
OYELEKE ISMAIL - PORTFOLIO WEBSITE DOCUMENTATION
========================================================================

Hi Oyeleke! This file is your guide to maintaining and updating your 
portfolio website. 

--- FOLDER STRUCTURE ---
1. index.html   -> The main structure (text, links, layout).
2. style.css    -> The design (colors, fonts, spacing).
3. script.js    -> The animations (mobile menu, typing text).
4. resume.pdf   -> Your CV file (Must be named exactly this!).
5. favicon.png  -> Your browser icon (Your photo or logo).
6. images/      -> Folder where you should keep certification badges.

========================================================================
HOW TO MAKE UPDATES
========================================================================

1. HOW TO ADD A NEW PROJECT
   ------------------------
   Open 'index.html' and scroll to the "Projects" section.
   Copy the code block below and paste it after the last project card
   inside the <div class="projects-grid"> container.

   <div class="project-card">
       <div class="card-content">
           <span class="tag tag-cloud">INFRASTRUCTURE</span> 
           
           <h3>Project Title Here</h3>
           
           <p class="project-desc">
               Write 1-2 sentences about what you built and the problem it solved.
           </p>
           
           <div class="tech-stack">
               <span>AWS Service</span><span>Language</span><span>Tool</span>
           </div>
           
           <div class="card-links">
               <a href="YOUR_GITHUB_LINK" target="_blank"><i class="fa-brands fa-github"></i> View Code</a>
           </div>
       </div>
   </div>
   2. HOW TO UPDATE YOUR RESUME
   -------------------------
   Simply delete the old 'resume.pdf' from this folder.
   Paste your new PDF file here and rename it to 'resume.pdf'.
   (No code changes needed!)


3. HOW TO CHANGE THE TYPING TEXT ("Hi, I'm...")
   --------------------------------------------
   Open 'script.js'.
   Look for Line 19: const textToType = "...";
   Change the text inside the quotes.


4. HOW TO ADD A NEW CERTIFICATION
   ------------------------------
   Open 'index.html' and find the "Certifications" section.
   Copy an existing <a href...> line and paste it where you want the new one.
   
   Template:
   <a href="CREDLY_LINK_HERE" target="_blank" class="cert-item">
       <div class="cert-placeholder"><i class="fa-solid fa-certificate"></i></div>
       <span>Name of Certification</span>
   </a>
   
   *Tip: To use a real image instead of an icon, replace the <div> line with:
   <img src="images/my-new-badge.png" alt="Badge Name">


5. HOW TO CHANGE COLORS
   --------------------
   Open 'style.css'. At the very top, you will see ":root".
   Change the hex codes to update the theme instantly.
   
   --primary-color: #0f172a;  (Dark Navy)
   --accent-color:  #2563eb;  (Blue)
   --aws-orange:    #FF9900;  (AWS Color)
   --dotnet-purple: #512BD4;  (.NET Color)


========================================================================
DEPLOYMENT CHECKLIST (AWS S3)
========================================================================
1. Create S3 Bucket (Enable Static Website Hosting).
2. Upload all files (html, css, js, pdf, png).
3. Set Permissions (Uncheck "Block all public access").
4. Add Bucket Policy (Allow "s3:GetObject" for public).
5. (Optional) Set up CloudFront & Route 53 for HTTPS.

Good luck, Cloud Engineer! 🚀