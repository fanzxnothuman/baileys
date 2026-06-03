# WhatsApp Baileys

<p align="center">
  <img src="https://files.catbox.moe/z33avx.png" alt="Thumbnail" />
</p>

WhatsApp Baileys is a robust open-source library engineered to empower developers in building sophisticated automation solutions and seamless WhatsApp integrations. Leveraging WebSocket technology — entirely browser-free — it delivers a comprehensive suite of capabilities including message management, chat handling, group administration, interactive messages, and dynamic action buttons for an elevated user experience.

Continuously developed and actively maintained, Baileys receives consistent updates to strengthen stability and overall performance. A primary area of focus is the refinement of pairing and authentication workflows, ensuring a more resilient and secure connection. Pairing procedures are fully customizable with user-defined codes, significantly reducing the likelihood of failures or unexpected disconnections.

This library is purpose-built for constructing enterprise-grade bots, chat automation pipelines, customer service platforms, and a wide spectrum of communication automation applications demanding both high reliability and feature completeness. Its lightweight, modular architecture ensures effortless integration across diverse systems and deployment environments.

---

### Key Features & Advantages

- Fully supports both automatic and custom pairing workflows
- Resolves longstanding pairing instability and disconnection issues
- Delivers interactive messages, action buttons, and dynamic menu rendering
- Intelligent session management with minimal overhead for sustained reliability
- Full compatibility with WhatsApp's latest multi-device architecture
- Lightweight, stable, and designed for seamless third-party integration
- Ideal for building bots, automation pipelines, and end-to-end communication solutions
- Thorough documentation and practical code examples to accelerate development

---

## Getting Started

Install the library through your preferred package manager and follow the configuration guide provided. The included example code offers a clear foundation for understanding each feature. Leverage session storage and interactive messaging capabilities to craft stable, production-ready solutions tailored to your specific requirements.

---

## Additional Functions

### Label Group

Assign a tag or label to a group member.

```javascript
await sock.setLabelGroup(jid, string);
```

---

### Retrieve Channel ID

Fetch the channel identifier from a given URL.

```javascript
await sock.newsletterFromUrl(url);
```

Response JSON:

```json
{
  "name": "Channel Name",
  "id": "Channel ID",
  "state": "Channel Status",
  "subscribers": "Subscriber Count",
  "verification": "UNVERIFIED",
  "creation_time": 1728547155,
  "description": "Channel Description"
}
```

---

### Check Banned Number

Verify whether a given number has been blocked or banned.

```javascript
sock.checkWhatsApp(jid);
```

---

## SendMessage Reference

### Status Mention — Group & Private

Dispatch a status mention to a group or private conversation.

```javascript
await sock.sendStatusMention(content, jid);
```

### Group Status Message (V2)

Send a group status using the Version 2 protocol.

```javascript
await sock.sendMessage(jid, {
  groupStatusMessage: {
    text: "Your group status message here.",
  },
});
```

### Album Message (Multiple Images)

Deliver multiple images as a single cohesive album.

```javascript
await sock.sendMessage(jid, {
  albumMessage: [
    {
      image: IMAGE,
      caption: "First image caption",
    },
    {
      image: { url: "YOUR_IMAGE_URL" },
      caption: "Second image caption",
    },
  ],
}, { quoted: m });
```

### Event Message

Compose and dispatch a WhatsApp event invitation.

```javascript
await sock.sendMessage(jid, {
  eventMessage: {
    isCanceled: false,
    name: "Your Event Name",
    description: "A brief description of your event.",
    location: {
      degreesLatitude: 0,
      degreesLongitude: 0,
      name: "Event Location",
    },
    joinLink: "https://call.whatsapp.com/video/your-link",
    startTime: "1763019000",
    endTime: "1763026200",
    extraGuestsAllowed: false,
  },
}, { quoted: m });
```

### Poll Result Message

Render poll results alongside their respective vote tallies.

```javascript
await sock.sendMessage(jid, {
  pollResultMessage: {
    name: "Your Poll Title",
    pollVotes: [
      {
        optionName: "Option A",
        optionVoteCount: "2"
      },
      {
        optionName: "Option B",
        optionVoteCount: "1"
      }
    ]
  }
}, { quoted: m });
```

### Simple Interactive Message

Send a straightforward interactive message featuring a copy-to-clipboard button.

```javascript
await sock.sendMessage(jid, {
  interactiveMessage: {
    header: "Message Header",
    title: "Message Title",
    footer: "telegram: @fanzxnothuman",
    buttons: [
      {
        name: "cta_copy",
        buttonParamsJson: JSON.stringify({
          display_text: "Copy Code",
          id: "123456789",
          copy_code: "YOUR_CODE_HERE"
        })
      }
    ]
  }
}, { quoted: m });
```

### Interactive Message with Native Flow

Send a feature-rich interactive message incorporating buttons, copy actions, and native flow elements.

```javascript
await sock.sendMessage(jid, {
  interactiveMessage: {
    header: "Message Header",
    title: "Message Title",
    footer: "telegram: @fanzxnothuman",
    image: { url: "https://example.com/image.jpg" },
    nativeFlowMessage: {
      messageParamsJson: JSON.stringify({
        limited_time_offer: {
          text: "Your promotional text here.",
          url: "https://t.me/fanzxnothuman",
          copy_code: "YOUR_CODE",
          expiration_time: Date.now() * 999
        },
        bottom_sheet: {
          in_thread_buttons_limit: 2,
          divider_indices: [1, 2, 3, 4, 5, 999],
          list_title: "List Title",
          button_title: "Button Label"
        },
        tap_target_configuration: {
          title: "Target Title",
          description: "Target description.",
          canonical_url: "https://t.me/fanzxnothuman",
          domain: "example.com",
          button_index: 0
        }
      }),
      buttons: [
        {
          name: "single_select",
          buttonParamsJson: JSON.stringify({
            has_multiple_buttons: true
          })
        },
        {
          name: "call_permission_request",
          buttonParamsJson: JSON.stringify({
            has_multiple_buttons: true
          })
        },
        {
          name: "single_select",
          buttonParamsJson: JSON.stringify({
            title: "Select an Option",
            sections: [
              {
                title: "Category",
                highlight_label: "Label",
                rows: [
                  {
                    title: "First Option",
                    description: "Option description.",
                    id: "row_1"
                  }
                ]
              }
            ],
            has_multiple_buttons: true
          })
        },
        {
          name: "cta_copy",
          buttonParamsJson: JSON.stringify({
            display_text: "Copy Code",
            id: "123456789",
            copy_code: "YOUR_CODE"
          })
        }
      ]
    }
  }
}, { quoted: m });
```

### Interactive Message with Thumbnail

Send an interactive message accompanied by a thumbnail image and a copy button.

```javascript
await sock.sendMessage(jid, {
  interactiveMessage: {
    header: "Message Header",
    title: "Message Title",
    footer: "telegram: @fanzxnothuman",
    image: { url: "https://example.com/image.jpg" },
    buttons: [
      {
        name: "cta_copy",
        buttonParamsJson: JSON.stringify({
          display_text: "Copy Code",
          id: "123456789",
          copy_code: "YOUR_CODE"
        })
      }
    ]
  }
}, { quoted: m });
```

### Product Message

Dispatch a product catalog message complete with merchant details and action buttons.

```javascript
await sock.sendMessage(jid, {
  productMessage: {
    title: "Product Name",
    description: "A concise description of the product.",
    thumbnail: { url: "https://example.com/image.jpg" },
    productId: "PROD001",
    retailerId: "RETAIL001",
    url: "https://example.com/product",
    body: "Full product details.",
    footer: "Special pricing available.",
    priceAmount1000: 50000,
    currencyCode: "IDR",
    buttons: [
      {
        name: "cta_url",
        buttonParamsJson: JSON.stringify({
          display_text: "Purchase Now",
          url: "https://example.com/buy"
        })
      }
    ]
  }
}, { quoted: m });
```

### Interactive Message with Document Buffer

Send an interactive message with a document loaded from the file system. **Note: Document attachments exclusively support buffer input.**

```javascript
await sock.sendMessage(jid, {
  interactiveMessage: {
    header: "Message Header",
    title: "Message Title",
    footer: "telegram: @fanzxnothuman",
    document: fs.readFileSync("./package.json"),
    mimetype: "application/pdf",
    fileName: "document.pdf",
    jpegThumbnail: fs.readFileSync("./thumbnail.jpeg"),
    contextInfo: {
      mentionedJid: [jid],
      forwardingScore: 777,
      isForwarded: false
    },
    externalAdReply: {
      title: "Your Bot Name",
      body: "Your bot description.",
      mediaType: 3,
      thumbnailUrl: "https://example.com/image.jpg",
      mediaUrl: "https://example.com",
      sourceUrl: "https://t.me/fanzxnothuman",
      showAdAttribution: true,
      renderLargerThumbnail: false
    },
    buttons: [
      {
        name: "cta_url",
        buttonParamsJson: JSON.stringify({
          display_text: "Telegram",
          url: "https://t.me/fanzxnothuman",
          merchant_url: "https://t.me/fanzxnothuman"
        })
      }
    ]
  }
}, { quoted: m });
```

### Interactive Message with Document Buffer (Minimal)

A streamlined variant without `contextInfo` or `externalAdReply`. **Note: Document attachments exclusively support buffer input.**

```javascript
await sock.sendMessage(jid, {
  interactiveMessage: {
    header: "Message Header",
    title: "Message Title",
    footer: "telegram: @fanzxnothuman",
    document: fs.readFileSync("./package.json"),
    mimetype: "application/pdf",
    fileName: "document.pdf",
    jpegThumbnail: fs.readFileSync("./thumbnail.jpeg"),
    buttons: [
      {
        name: "cta_url",
        buttonParamsJson: JSON.stringify({
          display_text: "Telegram",
          url: "https://t.me/fanzxnothuman",
          merchant_url: "https://t.me/fanzxnothuman"
        })
      }
    ]
  }
}, { quoted: m });
```

### Request Payment Message

Initiate a payment request with a custom background configuration and sticker attachment.

```javascript
let quotedType = m.quoted?.mtype || '';
let quotedContent = JSON.stringify({ [quotedType]: m.quoted }, null, 2);

await sock.sendMessage(jid, {
  requestPaymentMessage: {
    currency: 'IDR',
    amount: 10000000,
    from: m.sender,
    sticker: JSON.parse(quotedContent),
    background: {
      id: '100',
      fileLength: '0',
      width: 1000,
      height: 1000,
      mimetype: 'image/webp',
      placeholderArgb: 0xff00ffff,
      textArgb: 0xffffffff,
      subtextArgb: 0xffaa00ff
    }
  }
}, { quoted: m });
```

---

## Why WhatsApp Baileys?

This library stands out for its exceptional stability, comprehensive feature set, and a continuously refined pairing mechanism. It is the preferred choice for developers building professional-grade, secure WhatsApp automation solutions. Ongoing support for the latest WhatsApp capabilities ensures long-term compatibility and future-proofing.

---

### Technical Notes

- Custom pairing codes with proven stability and security
- Resolves known authentication and pairing failure edge cases
- Interactive messages and action buttons for sophisticated dynamic menus
- Automated, low-overhead session management for sustained uptime
- Full multi-device support aligned with WhatsApp's latest specifications
- Modular design enabling straightforward customization and extensibility
- Well-suited for bots, customer service automation, and enterprise communication tooling
- Subscribe to the official WhatsApp Channel for updates: [WhatsApp Channel](https://whatsapp.com/channel/0029VbA69WNDDmFMgxLdoA0U)

---

For complete documentation, installation instructions, and implementation references, visit the official repository and community forums. This library is under active development, with continuous improvements driven by real-world developer needs.

**Thank you for choosing WhatsApp Baileys as your WhatsApp automation foundation.**

---

### Contact

For inquiries, support, or collaboration opportunities:

- **Telegram**: [fanzxnothuman](https://t.me/fanzxnothuman)
- **WhatsApp Channel**: [WhatsApp Channel](https://whatsapp.com/channel/0029VbA69WNDDmFMgxLdoA0U)

### 🙌 Contributors

Recognition to the following contributors who have helped shape this project:

<table>
  <tr>
    <td align="center">
      <a href="https://github.com/fanzxnothuman">
        <img src="https://github.com/fanzxnothuman.png" width="80px;" style="border-radius:50%;" alt="Uploader"/>
        <br />
        <sub><b>Fantzy</b></sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/kiuur">
        <img src="https://github.com/kiuur.png" width="80px;" style="border-radius:50%;" alt="Developer"/>
        <br />
        <sub><b>KyuuRzy</b></sub>
      </a>
    </td>
  </tr>
</table>
