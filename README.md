# Sand---billing-

function makeQR(callback){
  const section = document.getElementById("billQR");
  section.innerHTML = "";

  const details = {
    "Registration ID": getValue("regId"),
    "Consumer Name": getValue("consumerName"),
    "Consumer Mobile No": getValue("consumerMobile"),
    "Construction Name": getValue("constructionName"),
    "Registration Date & Time": formatDate(getValue("regDateTime")),
    "Registration Type": getValue("regType"),
    "Registration QTY (in MT)": getValue("regQty"),
    "Registration Address": getValue("regAddress")
  };

  const data = JSON.stringify(details);
  const qr = document.createElement("img");
  qr.alt = "Registration Details QR Code";

  qr.onload = function(){
    const heading = document.createElement("div");
    heading.style.fontSize = "12px";
    heading.style.fontWeight = "bold";
    heading.style.marginBottom = "5px";
    heading.textContent = "Registration Details QR";

    section.prepend(heading);

    const thanks = document.createElement("div");
    thanks.id = "qrThanks";
    thanks.textContent = "Thank You";
    section.appendChild(thanks);

    if(callback) callback(true);
  };

  qr.onerror = function(){
    section.innerHTML = "QR కోడ్ తయారు కాలేదు. ఇంటర్నెట్ తనిఖీ చేయండి.";
    if(callback) callback(false);
  };

  qr.src = "https://api.qrserver.com/v1/create-qr-code/?size=350x350&margin=1&data=" + encodeURIComponent(data);
  section.appendChild(qr);
}
