```javascript
[Item]PaperNote

<table>
  <tr>
    <td style="padding:8px; text-align:center; vertical-align:middle;">
      <b><center>${topItem.getField("title")}</center></b>
    </td>
  </tr>
  <tr>
    <td style="padding:8px;">
      <b>Author:</b> ${topItem.getCreators().slice(0, 10).map((v) => v.firstName + " " + v.lastName).join("; ") + (topItem.getCreators().length > 10 ? "; et al." : ";")}
    </td>
  </tr>

  <tr>
    <td style="padding:8px;">
      <b>Journal:</b> #${topItem.getField('publicationTitle').replace(/\s+/g, '-')}
    </td>
  </tr>

  <tr>
    <td style="padding:8px;">
      <b>Publication Date: </b> ${topItem.getField("date").split('T')[0]}
    </td>
  </tr>

  <tr>
    <td style="padding:8px;">
      <b>Key Word: </b> ${topItem.getTags().slice(0, 10).map((v) => `#${v.tag.replace(/\s+/g, '-')}`).join("; ")}
    </td>
  </tr>

  <tr>
    <td style="padding:8px;">
      ${(() => {
        const attachments = Zotero.Items.get(topItem.getAttachments());
        const pdf = attachments.filter((i) => i.isPDFAttachment());
        if (pdf && pdf.length > 0) {
          return `<b>Local Link: </b><a href="zotero://open-pdf/0_${pdf[0].key}">${pdf[0].getFilename()}</a>`;
        } else if (attachments && attachments.length > 0) {
          return `<b>Local Link: </b><a href="zotero://open-pdf/0_${attachments[0].key}">${attachments[0].getFilename()}</a>`;
        } else {
          return `<b>Local Link: </b>`;
        }
      })()}
    </td>
  </tr>
  
  <tr>
    <td style="padding:8px;">
      ${(() => {
        const doi = topItem.getField("DOI");
        if (doi) {
          return `<b>DOI: </b><a href="https://doi.org/${topItem.getField('DOI')}">${topItem.getField('DOI')}</a>`;
        } else {
          return `<b>URL: </b><a href="${topItem.getField('url')}">${topItem.getField('url')}</a>`;
        }
      })()}
    </td>
  </tr>
  
  <tr>
    <td style="padding:8px;">
      ${(() => {
        const abstractTranslation = topItem.getField('abstractTranslation');
        if (abstractTranslation) {
          return `<b>Abstract Translation:  </b> ${abstractTranslation}`;
        } else {
          return `<b>Abstract:  </b> ${topItem.getField('abstractNote')}`;
        }
      })()}
    </td>
  </tr>

</table>

<span>
    <h1>🌱 Core</h1>
</span>
<blockquote>Tips: What are the article's contributions, innovations and shortcomings</blockquote>
<h2>🌻 Content</h2>
<p></p>
<h2>💐 Research Gap & Innovations</h2>
<p></p>
<h2>🍂 Shortcomings</h2>
<p></p>

<span>
    <h1>🌳 Content</h1>
</span>
<blockquote>Tips: What are the article's methods, experimental frameworks, and conclusions(figures, tables)</blockquote>
<h2>🐢 Data</h2>
<p></p>
<h2>🐲 Method</h2>
<p></p>
<h2>🐉 Experiment</h2>
<p></p>
<h2>🦥 Conclusion</h2>
<p></p>

<span>
    <h1>🍀 Summary</h1>
</span>
<blockquote>Tips: What are the article's key points, insights gained, and potential improvements</blockquote>
<h2>🐼 Key Records</h2>
<p></p>
<h2>🐻‍❄️ Inspiration</h2>
<p></p>
<h2>🐻 To be resolved</h2>
<p></p>
```

```javascript
ExportMDFileHeaderV2
${{
  let header = {};
  header.tags = '#论文';
  header.noteTime = new Date().toLocaleString();
  return JSON.stringify(header);
}}$
```

```javascript
[Item]术语卡
<!-- Title -->
<h1 style="color:#193c47; background-color:#eef9fd; padding:8px;">
  ${(() => {
    const date = topItem.getField("date").split('T')[0];
    return `'术语&${date}&name'`
  })()}
</h1>

<p></p>
<h3>⚙️ Explanation</h3>
<p></p>
```