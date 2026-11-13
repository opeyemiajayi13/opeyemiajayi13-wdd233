const membersContainer = document.querySelector("#members-container");
const gridButton = document.querySelector("#grid-button");
const listButton = document.querySelector("#list-button");
const memberCount = document.querySelector("#member-count");

const menuButton = document.querySelector("#menu-button");
const mainNav = document.querySelector("#main-nav");

// Display the current copyright year
document.querySelector("#copyright-year").textContent =
    new Date().getFullYear();

// Display the last modification date
const modifiedDate = new Date(document.lastModified);

document.querySelector("#last-modified").textContent =
    modifiedDate.toLocaleString();

// Mobile navigation
menuButton.addEventListener("click", () => {
    const isOpen = mainNav.classList.toggle("open");

    menuButton.setAttribute("aria-expanded", isOpen);
    menuButton.setAttribute(
        "aria-label",
        isOpen ? "Close navigation menu" : "Open navigation menu"
    );
});

// Fetch business information from JSON
async function getMembers() {
    try {
        const response = await fetch("data/members.json");

        if (!response.ok) {
            throw new Error("Unable to load member information.");
        }

        const members = await response.json();

        displayMembers(members);

    } catch (error) {
        membersContainer.innerHTML =
            '<p class="empty-message">Business information could not be loaded. Please try again later.</p>';

        console.error(error);
    }
}

// Display all business members
function displayMembers(members) {

    membersContainer.innerHTML = "";

    memberCount.textContent =
        `${members.length} businesses in our directory`;

    members.forEach((member) => {

        const card = document.createElement("article");
        card.classList.add("member-card");

        const image = document.createElement("img");
        image.src = `images/${member.image}`;
        image.alt = `${member.name} business`;
        image.loading = "lazy";

        const information = document.createElement("div");
        information.classList.add("member-info");

        const name = document.createElement("h3");
        name.textContent = member.name;

        const address = document.createElement("p");
        address.textContent = `Address: ${member.address}`;

        const phone = document.createElement("p");
        phone.textContent = `Phone: ${member.phone}`;

        const level = document.createElement("span");
        level.classList.add("membership");
        level.textContent = getMembership(member.membership);

        const description = document.createElement("p");
        description.textContent = member.description;

        const website = document.createElement("a");
        website.href = member.website;
        website.textContent = "Visit Website";
        website.classList.add("website-link");
        website.target = "_blank";
        website.rel = "noopener noreferrer";

        information.append(
            name,
            address,
            phone,
            description,
            level,
            website
        );

        card.append(image, information);

        membersContainer.appendChild(card);
    });
}

// Convert membership numbers to readable names
function getMembership(level) {

    if (level === 3) {
        return "Gold Member";
    }

    if (level === 2) {
        return "Silver Member";
    }

    return "Member";
}

// Grid view
gridButton.addEventListener("click", () => {

    membersContainer.classList.remove("members-list");
    membersContainer.classList.add("members-grid");

    gridButton.classList.add("active");
    listButton.classList.remove("active");

    gridButton.setAttribute("aria-pressed", "true");
    listButton.setAttribute("aria-pressed", "false");
});

// List view
listButton.addEventListener("click", () => {

    membersContainer.classList.remove("members-grid");
    membersContainer.classList.add("members-list");

    listButton.classList.add("active");
    gridButton.classList.remove("active");

    listButton.setAttribute("aria-pressed", "true");
    gridButton.setAttribute("aria-pressed", "false");
});

// Start loading the directory
getMembers();