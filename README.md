
function makeQR(callback){
  const section = document.getElementById("billQR");
  section.innerHTML = "";

  const details = {
    regId: getValue("regId"),
    consumerName: getValue("consumerName"),
    consumerMobile: getValue("consumerMobile"),
    constructionName: getValue("constructionName"),
    regDateTime: formatDate(getValue("regDateTime")),
    regType: getValue("regType"),
    regQty: getValue("regQty"),
    regAddress: getValue("regAddress")
  };

  const encoded = btoa(
    unescape(encodeURIComponent(JSON.stringify(details)))
  );

  const url = REGISTRATION_URL + "?registration=" + encoded;

  const img = document.createElement("img");
  img.alt = "Registration Details QR Code";

  img.onload = function(){
    const thanks = document.createElement("div");
    thanks.id = "qrThanks";
    thanks.textContent = "Thank You";
    section.appendChild(thanks);
    if(callback) callback(true);
  };

  img.onerror = function(){
    section.innerHTML = "QR కోడ్ తయారు కాలేదు.";
    if(callback) callback(false);
  };

  img.src = "https://api.qrserver.com/v1/create-qr-code/?size=350x350&margin=1&data=" +
            encodeURIComponent(url);

  section.appendChild(img);
}
