# Hackathon-Project-Ideas
// Dark Mode Toggle
const darkModeToggle = document.getElementById("darkModeToggle");
darkModeToggle.addEventListener("click", () => {
    document.body.classList.toggle("dark-mode");
});

// Drag and Drop Functionality
const draggables = document.querySelectorAll(".draggable");
const container = document.querySelector(".drag-container");

draggables.forEach(draggable => {
    draggable.addEventListener("dragstart", () => {
        draggable.classList.add("dragging");
    });
    draggable.addEventListener("dragend", () => {
        draggable.classList.remove("dragging");
    });
});

container.addEventListener("dragover", (e) => {
    e.preventDefault();
    const afterElement = getDragAfterElement(container, e.clientY);
    const dragging = document.querySelector(".dragging");
    if (afterElement == null) {
        container.appendChild(dragging);
    } else {
        container.insertBefore(dragging, afterElement);
    }
});

function getDragAfterElement(container, y) {
    const draggableElements = [...container.querySelectorAll(".draggable:not(.dragging)")];
    return draggableElements.reduce((closest, child) => {
        const box = child.getBoundingClientRect();
        const offset = y - box.top - box.height / 2;
        if (offset < 0 && offset > closest.offset) {
            return { offset: offset, element: child };
        } else {
            return closest;
        }
    }, { offset: Number.NEGATIVE_INFINITY }).element;
}

// AI Resume Generation
const resumeForm = document.getElementById("resumeForm");
const resumeOutput = document.getElementById("resumeOutput");

resumeForm.addEventListener("submit", (e) => {
    e.preventDefault();
    const name = document.getElementById("name").value;
    const title = document.getElementById("title").value;
    const email = document.getElementById("email").value;
    const linkedin = document.getElementById("linkedin").value;
    const github = document.getElementById("github").value;
    const experience = document.getElementById("experience").value;
    const skills = document.getElementById("skills").value;

    resumeOutput.innerHTML = `
        <h3>${name}</h3>
        <p><strong>Title:</strong> ${title}</p>
        <p><strong>Email:</strong> ${email}</p>
        <p><strong>LinkedIn:</strong> <a href="https://www.linkedin.com/in/${linkedin}" target="_blank">${linkedin}</a></p>
        <p><strong>GitHub:</strong> <a href="${github}" target="_blank">${github}</a></p>
        <p><strong>Experience:</strong> ${experience}</p>
        <p><strong>Skills:</strong> ${skills}</p>
    `;
});
 
