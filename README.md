# MdGPT

Welcome to MarkdownGPT or MdGPT. This nifty little bookmark lets you save your chats to markdown so you can insert it into markdown apps like obsidian.

## Instructions:

1. Create a new bookmark in your browser.
2. Edit the bookmark's URL field and replace its value with the following code:

```javascript
javascript:(function() {
  function h(html) {
    return html.replace(/<p>/g, '\n\n').replace(/<\/p>/g, '').replace(/<b>/g, '**').replace(/<\/b>/g, '**').replace(/<i>/g, '_').replace(/<\/i>/g, '_').replace(/<code[^>]*>/g, (match) => {
      const lm = match.match(/class="[^"]*language-([^"]*)"/);
      return lm ? '\n```' + lm[1] + '\n' : '```';
    }).replace(/<\/code[^>]*>/g, '```').replace(/<[^>]*>/g, '').replace(/Copy code/g, '').replace(/This content may violate our content policy. If you believe this to be in error, please submit your feedback — your input will aid our research in this area./g, '').trim();
  }
  const e = document.querySelectorAll(".text-base");
  let t = "";
  for (const s of e) {
    if (s.querySelector(".whitespace-pre-wrap")) {
      t += t == "" ? "" : "--------\n";
      t += `**${s.querySelectorAll('img').length > 1 ? s.querySelectorAll('img')[1].alt : 'ChatGPT'}**: ${h(s.querySelector(".whitespace-pre-wrap").innerHTML)}\n\n`;
    }
  }
  const o = document.createElement("a");
  o.download = (document.querySelector(".pr-14.bg-gray-800")?.innerText || "Conversation with ChatGPT") + ".md";
  o.href = URL.createObjectURL(new Blob([t]));
  o.style.display = "none";
  document.body.appendChild(o);
  o.click();
})();

```

1. Save the bookmark.
2. Open a page that contains a conversation with ChatGPT.
3. Click the bookmark to run the code and download the conversation as a Markdown file.
