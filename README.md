
<script>
const REGISTRATION_URL =
  "https://chashok1629-tech.github.io/Sand---billing-/";

function makeQR() {
  const section = document.getElementById("billQR");
  if (!section) {
    alert("billQR section not found");
    return;
  }

  const details = {
    regId: document.getElementById("regId")?.value || "",
    consumerName: document.getElementById("consumerName")?.value || "",
    consumerMobile: document.getElementById("consumerMobile")?.value || "",
    constructionName: document.getElementById("constructionName")?.value || "",
    regDateTime: document.getElementById("regDateTime")?.value || "",
    regType: document.getElementById("regType")?.value || "",
    regQty: document.getElementById("regQty")?.value || "",
    regAddress: document.getElementById("regAddress")?.value || ""
  };

  const encoded = btoa(
    unescape(encodeURIComponent(JSON.stringify(details)))
  );

  const url =
    REGISTRATION_URL + "?registration=" +
    encodeURIComponent(encoded);

  const sectionURL =
    "https://api.qrserver.com/v1/create-qr-code/?size=350x350&data=" +
    encodeURIComponent(url);

  section.innerHTML = "";

  const img = document.createElement("img");
  img.src = sectionURL;
  img.alt = "Registration Details QR Code";
  img.style.width = "250px";
  img.style.maxWidth = "100%";

  img.onload = function () {
    section.appendChild(img);

    const link = document.createElement("a");
    link.href = sectionURL;
    link.download = "Sand-Registration-QR.png";
    link.textContent = "Download QR Code";
    link.style.display = "block";
    link.style.marginTop = "10px";

    section.appendChild(link);
  };

  img.onerror = function () {
    section.textContent = "QR Code తయారు కాలేదు. Internet చెక్ చేయండి.";
  };
}
</script>
