document.addEventListener("DOMContentLoaded", () => {
    const themeToggle = document.querySelector("#theme-toggle");
    const toggleSwitch = themeToggle.querySelector(".toggle-switch");
    const sunIcon = themeToggle.querySelector(".sun");
    const moonIcon = themeToggle.querySelector(".moon");

    const toggleTheme = () => {
        document.body.classList.toggle("dark");
        updateLocalStorage();
        updateToggleKnob();
    };

    const updateLocalStorage = () => {
        if (document.body.classList.contains("dark")) {
            localStorage.setItem("theme", "dark");
        } else {
            localStorage.setItem("theme", "light");
        }
    };

    const updateToggleKnob = () => {
        if (document.body.classList.contains("dark")) {
            toggleSwitch.querySelector(".toggle-knob").style.transform = "translateX(26px)";
            sunIcon.style.display = "none";
            moonIcon.style.display = "block";
        } else {
            toggleSwitch.querySelector(".toggle-knob").style.transform = "translateX(0)";
            sunIcon.style.display = "block";
            moonIcon.style.display = "none";
        }
    };

    themeToggle.addEventListener("click", toggleTheme);

    // Apply theme from local storage on load
    if (localStorage.getItem("theme") === "dark") {
        document.body.classList.add("dark");
    }
    updateToggleKnob();

    // Smooth scroll for internal links
    document.querySelectorAll('a[href^="#"]').forEach(anchor => {
        anchor.addEventListener("click", function(e) {
            e.preventDefault();
            document.querySelector(this.getAttribute("href")).scrollIntoView({
                behavior: "smooth"
            });
        });
    });

    // Add a scroll-to-top button
    const scrollToTopButton = document.createElement("button");
    scrollToTopButton.textContent = "⬆️";
    scrollToTopButton.classList.add("scroll-to-top");
    document.body.appendChild(scrollToTopButton);

    scrollToTopButton.addEventListener("click", () => {
        window.scrollTo({
            top: 0,
            behavior: "smooth"
        });
    });

    window.addEventListener("scroll", () => {
        if (window.scrollY > 200) {
            scrollToTopButton.classList.add("visible");
        } else {
            scrollToTopButton.classList.remove("visible");
        }
    });
});
