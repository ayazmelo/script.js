document.addEventListener("DOMContentLoaded", function () {

    const chatButton = document.getElementById("ayaz-chat-button");
    const chatBox = document.getElementById("ayaz-chat-box");
    const closeButton = document.getElementById("ayaz-close");
    const messages = document.getElementById("ayaz-messages");
    const options = document.getElementById("ayaz-options");
    const input = document.getElementById("ayaz-input");
    const sendButton = document.getElementById("ayaz-send");

    if (!chatButton || !chatBox || !messages || !options) return;

    const faqs = [
        {
            question: "Ayaz Melo ڇا آهي؟",
            answer: "اياز ميلو سنڌ جي نامياري شاعر شيخ اياز جي فڪر، سنڌي ٻولي، ادب، ثقافت ۽ فن کي ملهائڻ وارو ادبي ۽ ثقافتي ميلو آهي."
        },
        {
            question: "When is Ayaz Melo 2026?",
            answer: "Ayaz Melo 2026 will be held from 19 to 21 December 2026."
        },
        {
            question: "ميلو ڪٿي ٿيندو؟",
            answer: "ميلو جي هنڌ بابت حتمي اعلان اڃا نه ٿيو آهي. سرڪاري اعلان لاءِ ويب سائيٽ ۽ سوشل ميڊيا سان رابطي ۾ رهو."
        },
        {
            question: "How can I register?",
            answer: "Registration details and the official registration facility will be available through the website."
        },
        {
            question: "Volunteer ڪيئن بڻجي سگهجي ٿو؟",
            answer: "رضاڪارن جي رجسٽريشن ۽ چونڊ بابت معلومات لاءِ آرگنائيزنگ ٽيم سان رابطو ڪريو."
        },
        {
            question: "Book Stall Booking",
            answer: "ڪتابن جي اسٽال جي بکنگ بابت تفصيل ۽ رهنمائي لاءِ آرگنائيزنگ ٽيم سان رابطو ڪريو."
        },
        {
            question: "Contact Number",
            answer: "توهان اسان سان هن نمبر تي رابطو ڪري سگهو ٿا: 03422564593"
        }
    ];

    function addMessage(text, sender) {
        const message = document.createElement("div");
        message.className = "ayaz-message " + sender;
        message.textContent = text;
        messages.appendChild(message);
        messages.scrollTop = messages.scrollHeight;
    }

    function showWelcome() {
        addMessage(
            "ڀلي ڪري آيا! اياز ميلو 2026 بابت معلومات لاءِ هيٺ ڏنل سوالن مان چونڊيو يا پنهنجو سوال لکو.",
            "ayaz-bot"
        );
    }

    function showOptions() {
        options.innerHTML = "";

        faqs.forEach(function (faq) {
            const button = document.createElement("button");
            button.className = "ayaz-option";
            button.textContent = faq.question;

            button.addEventListener("click", function () {
                addMessage(faq.question, "ayaz-user");
                addMessage(faq.answer, "ayaz-bot");
            });

            options.appendChild(button);
        });
    }

    function getAnswer(question) {
        const q = question.toLowerCase();

        if (q.includes("date") || q.includes("when") || q.includes("تاريخ") || q.includes("ڪڏهن")) {
            return "Ayaz Melo 2026 جون 19، 20 ۽ 21 ڊسمبر 2026 تي منعقد ٿيندو.";
        }

        if (q.includes("venue") || q.includes("where") || q.includes("جڳھ") || q.includes("ڪٿي")) {
            return "ميلو جي هنڌ بابت حتمي اعلان اڃا نه ٿيو آهي. سرڪاري اعلان جو انتظار ڪريو.";
        }

        if (q.includes("register") || q.includes("registration") || q.includes("رجسٽريشن")) {
            return "رجسٽريشن بابت معلومات لاءِ ويب سائيٽ جي Registration Section ڏسو.";
        }

        if (q.includes("volunteer") || q.includes("رضاڪار")) {
            return "رضاڪارن بابت معلومات لاءِ آرگنائيزنگ ٽيم سان رابطو ڪريو.";
        }

        if (q.includes("stall") || q.includes("book") || q.includes("اسٽال") || q.includes("ڪتاب")) {
            return "ڪتابن ۽ ثقافتي اسٽالن جي بکنگ لاءِ آرگنائيزنگ ٽيم سان رابطو ڪريو.";
        }

        if (q.includes("contact") || q.includes("phone") || q.includes("رابطو") || q.includes("نمبر")) {
            return "رابطي لاءِ فون يا واٽس ايپ: 03422564593";
        }

        if (q.includes("ayaz") || q.includes("اياز") || q.includes("melo") || q.includes("ميلو")) {
            return "اياز ميلو سنڌ جي ادب، ٻولي، ثقافت ۽ شيخ اياز جي فڪر کي ملهائڻ وارو ادبي ۽ ثقافتي ميلو آهي.";
        }

        return "مهرباني ڪري وڌيڪ معلومات لاءِ اسان جي آرگنائيزنگ ٽيم سان رابطو ڪريو: 03422564593";
    }

    function sendMessage() {
        const question = input.value.trim();

        if (!question) return;

        addMessage(question, "ayaz-user");

        const answer = getAnswer(question);

        setTimeout(function () {
            addMessage(answer, "ayaz-bot");
        }, 400);

        input.value = "";
    }

    chatButton.addEventListener("click", function () {
        chatBox.classList.toggle("active");

        if (messages.children.length === 0) {
            showWelcome();
            showOptions();
        }
    });

    if (closeButton) {
        closeButton.addEventListener("click", function () {
            chatBox.classList.remove("active");
        });
    }

    if (sendButton) {
        sendButton.addEventListener("click", sendMessage);
    }

    if (input) {
        input.addEventListener("keydown", function (event) {
            if (event.key === "Enter") {
                sendMessage();
            }
        });
    }

});
