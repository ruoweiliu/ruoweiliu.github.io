---
layout: single
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

## Upload / Replace CV (owner only)

To upload a new CV PDF directly to this repository, you can use the form below. This uses the GitHub REST API to create or update a file at `files/CV.pdf` in this repository. You must supply a GitHub Personal Access Token with `repo` scope. Keep your token private — anyone who has it can modify the repository.

Note: This is an owner-only convenience. If you prefer, you can also upload `files/CV.pdf` via the GitHub web UI or push it in a commit.

<form id="cvForm">
  <label for="token">GitHub Personal Access Token (repo scope):</label><br>
  <input type="password" id="token" style="width: 100%;" placeholder="ghp_..." required><br><br>

  <label for="cvfile">Select CV PDF file:</label><br>
  <input type="file" id="cvfile" accept="application/pdf" required><br><br>

  <button type="button" id="uploadBtn">Upload CV to Repository</button>
</form>

<p id="cvStatus"></p>

<script>
async function getExistingFileSha(token) {
  const owner = 'ruoweiliu';
  const repo = 'ruoweiliu.github.io';
  const path = 'files/CV.pdf';
  const url = `https://api.github.com/repos/${owner}/${repo}/contents/${encodeURIComponent(path)}`;
  const resp = await fetch(url, { headers: { Authorization: 'token ' + token } });
  if (resp.status === 200) {
    const data = await resp.json();
    return data.sha;
  }
  return null;
}

document.getElementById('uploadBtn').addEventListener('click', async () => {
  const token = document.getElementById('token').value.trim();
  const fileInput = document.getElementById('cvfile');
  const status = document.getElementById('cvStatus');
  if (!token) { status.textContent = 'Please provide a GitHub token.'; return; }
  if (!fileInput.files || fileInput.files.length === 0) { status.textContent = 'Please select a PDF file.'; return; }

  const file = fileInput.files[0];
  if (file.type !== 'application/pdf') { status.textContent = 'Please select a PDF file.'; return; }

  status.textContent = 'Reading file...';
  const reader = new FileReader();
  reader.onload = async () => {
    const base64 = btoa(reader.result);
    status.textContent = 'Checking existing file...';
    const sha = await getExistingFileSha(token);
    const owner = 'ruoweiliu';
    const repo = 'ruoweiliu.github.io';
    const path = 'files/CV.pdf';
    const url = `https://api.github.com/repos/${owner}/${repo}/contents/${encodeURIComponent(path)}`;
    const body = {
      message: sha ? 'Update CV.pdf' : 'Add CV.pdf',
      content: base64,
      branch: 'master'
    };
    if (sha) body.sha = sha;

    status.textContent = 'Uploading to GitHub...';
    const resp = await fetch(url, {
      method: 'PUT',
      headers: {
        Authorization: 'token ' + token,
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(body)
    });
    if (resp.ok) {
      status.textContent = 'Upload successful! File is now in `files/CV.pdf`.';
    } else {
      const text = await resp.text();
      status.textContent = 'Upload failed: ' + resp.status + ' ' + text;
    }
  };
  reader.readAsBinaryString(file);
});
</script>
