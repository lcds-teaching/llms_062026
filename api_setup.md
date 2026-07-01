# API Setup for Lab Three: Gemini

Lab Three uses the Google Gemini API only.

The simplest setup is to paste a temporary key directly into the notebook:

```python
GEMINI_API_KEY = "paste_key_here"
```

Students can use their own free-tier Gemini key. Instructors can use a separate Tier 1 prepay billing key for live demos that need more calls.

Do not commit or share a notebook that contains a real key.

## Getting a Gemini Key

1. Go to Google AI Studio: https://aistudio.google.com/app/apikey
2. Create or select an API key.
3. Paste it into `GEMINI_API_KEY` in Setup 1 of `Labs/Lab_3.ipynb`.
4. Run the setup cells from the top of the notebook.

The student notebook defaults to:

```python
GEMINI_MODEL = "gemini-2.5-flash"
```

If that model is unavailable for your account, replace it with another Gemini model name supplied by your instructor.

## Instructor Demo Quota

For an instructor-led live demo, use the instructor's Tier 1 prepay billing project rather than a student free-tier key. Estimate the live-call budget before class:

```text
needed calls = students * calls per student + instructor demo calls + retry buffer
```

Students should still use their own free-tier keys unless the instructor explicitly provides a class demo key. If a student sees a `429` error, they should wait and rerun later, or reduce the number of live calls they run.

## Safety Checklist

- Paste the key only into your own working copy of the notebook.
- Do not upload a completed notebook with a real key still in it.
- If a key is exposed, delete or rotate it in Google AI Studio.
- Remote API calls use quota and may incur cost.
- Revoke or delete any instructor demo key after the teaching session.
