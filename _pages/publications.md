---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---

{% if site.author.googlescholar %}
  <p>
  You can also find my articles on <a href="{{site.author.googlescholar}}">my Google Scholar profile</a>. 
  </p>
  <p>
  * denotes equal contribution.
  </p>  
{% endif %}

{% include base_path %}

<!-- Embedded CSS for Publication Styling -->  
<style>  
.publication {  
    border: 1px solid #e0e0e0; /* Light grey border */  
    padding: 10px; /* Padding around content */  
    margin: 10px 0; /* Margin around the publication block */  
    border-radius: 10px; /* Rounded corners */  
    background-color: #ffffff; /* White background */  
    box-shadow: 0px 0px 15px rgba(0,0,0,0.05); /* Subtle shadow */  
    display: flex; /* Flex display to align items horizontally */  
    flex-direction: row-reverse; /* Reverse the row to place image on right */  
}  

.pub-image-wrapper {  
    flex-shrink: 0; /* Prevent the image from shrinking */  
    margin-left: 10px; /* Space between image and content */  
    max-width: 40%
}  

.pub-image-wrapper img {  
    display: block; /* Ensure image is block-level */  
    width: 100%; /* Set a fixed width for the image */  
    border-radius: 8px; /* Rounded corners */  
}  

.pub-content-wrapper {  
    flex-grow: 1; /* Allow content to grow and take up remaining space */  
}  

.pub-title a {  
    font-size: 1.5em; /* Larger font size for title */  
    font-weight: bold; /* Bold font */  
    text-decoration: none; /* Remove underline */  
    color: #333; /* Dark color */  
}  

.pub-title a:hover {  
    color: #007BFF; /* Blue on hover */  
}  

.pub-author {  
    font-size: 1em;  
    color: #666; /* Grey text color */  
    margin-bottom: 5px;  
}  

.pub-author .highlight {  
    text-decoration: underline;  
    font-weight: bold;  
}  

.pub-venue {  
    display: inline-block;  
    background-color: #f1f1f1; /* Light grey background */  
    border: 1px solid #ddd; /* Light border */  
    padding: 2px 8px; /* Reduced padding */  
    margin: 5px 0; /* Margin */  
    border-radius: 8px; /* Rounded corners */  
    font-size: 0.9em; /* Smaller font size */  
    font-weight: bold; /* Bold font */  
    color: #333; /* Text color */  
    white-space: nowrap; /* Prevent wrapping */  
}  

.pub-tag {  
    display: inline-block;  
    background-color: #007BFF; /* Blue background */  
    color: #ffffff; /* White text */  
    padding: 5px 10px; /* Padding */  
    margin: 5px 2px; /* Margin */  
    border-radius: 12px; /* Rounded corners */  
    font-size: 0.875em; /* Slightly smaller font size */  
    text-align: center; /* Center the text */  
}  

.pub-misc a {  
    color: #333;  
    text-decoration: none;  
    font-weight: bold;  
}  

.pub-misc a:hover {  
    color: #0056b3;  
}  

.abstract-box {  
    display: none; /* Initially hidden */  
    background-color: #f9f9f9; /* Light grey background */  
    border: 1px solid #ccc; /* Light grey border */  
    padding: 15px; /* Padding around text */  
    margin: 10px 0; /* Margin above and below */  
    border-radius: 5px; /* Rounded corners */  
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1); /* Optional: subtle shadow */  
    white-space: normal; /* Ensures normal text wrapping */  
    word-wrap: break-word;  
    overflow-wrap: break-word;  
}  

/* Responsive Design */  
@media (max-width: 768px) {  
    .publication {  
        padding: 8px; /* Reduce padding */  
        flex-direction: column-reverse; /* Stack items vertically on small screens */  
    }  

    .pub-image-wrapper {  
        margin-left: 0;  
        margin-right: 0;  
        margin-top: 10px; /* Reduce space between image and content on small screens */  
        max-width: 100%; /* Image takes full width on small screens */  
    } 

    .pub-title a {  
        font-size: 1.2em; /* Smaller font size */  
    }  

    .pub-venue {  
        font-size: 0.9em; /* Smaller font size */  
    }  

    .pub-tag {  
        font-size: 0.75em; /* Smaller font size */  
    }  
}  
</style>  

<!-- Toggle Abstract Script -->  
<script type="text/javascript">  
    function toggle(id) {  
        var element = document.getElementById(id);  
        if (element.style.display === "none") {  
            element.style.display = "block";  
        } else {  
            element.style.display = "none";  
        }  
    }  
</script>

{% for post in site.publications reversed %}
  {% include archive-single-pub.html %}
{% endfor %}
