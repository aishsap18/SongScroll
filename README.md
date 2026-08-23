# 🎵 SongScroll

SongScroll is an intelligent, auto-scrolling teleprompter designed specifically for musicians and live performers. It uses advanced pitch and volume detection to listen to your instrument (like a guitar) and automatically scrolls your sheet music or notes exactly as you play.

Gone are the days of hastily swiping at your iPad mid-song!

## ✨ Features

*   **🎙️ Pluck Detection (Note Follow):** Uses your device's microphone to listen to your instrument. It counts the notes you play on each line and automatically scrolls to the next line when you finish.
*   **📄 PDF Canvas Mode:** Renders your original PDF exactly as it looks. The scroll speed adapts to your playing volume, and it automatically boosts the scroll speed during pitch slides/bends!
*   **✏️ Text Editor Mode:** Intelligently extracts lyrics and chords from your PDF, perfectly aligning them using a custom Tab-Stop grouping algorithm. You can manually edit the text, and SongScroll will permanently save your edits to the cloud.
*   **☁️ Cloud Library:** Features a built-in login system powered by Supabase. Any PDF you upload is saved to your personal library so you can access it anytime across devices.
*   **🎨 Dark Mode UI:** A beautiful, frosted-glass dark theme (#2d313a) designed to be easy on the eyes in dark stage environments.

## 🚀 How it Works

1.  **Sign Up / Login:** Create a free account or log in.
2.  **Upload:** Click Browse PDF to upload a PDF of your song's lyrics and chords.
3.  **Choose a Mode:**
    *   **PDF View:** See your original document. Play louder to scroll faster.
    *   **Text Editor:** See a clean, extracted text view. The app listens for distinct plucks and advances line-by-line as you play.
4.  **Perform:** Hit Start Listening, grab your instrument, and start playing. SongScroll will follow along!

## 🛠️ Tech Stack

SongScroll is built entirely as a lightweight, lightning-fast client-side application.

*   **Frontend:** HTML5, CSS3, Vanilla JavaScript (No heavy frameworks!)
*   **PDF Processing:** pdf.js (Mozilla)
*   **Audio Processing:** Web Audio API (AnalyserNode, Pitch detection)
*   **Backend & Auth:** Supabase (Auth, Storage Buckets)

## ⚙️ Local Setup

If you want to run SongScroll locally for development:

1.  Clone this repository:
    `ash
    git clone https://github.com/aishsap18/SongScroll.git
    cd SongScroll
    `
2.  Serve the directory using any local web server. (e.g., using Node's http-server):
    `ash
    npx http-server . -p 8080 -c-1
    `
3.  Open http://localhost:8080 in your browser.

*Note: For the microphone features to work, you must access the app via localhost or over a secure HTTPS connection.*

## 🔒 Supabase Configuration

To use the cloud features (Auth and Library), you need your own Supabase project:

1.  Create a Supabase project and get your Anon API key and URL.
2.  Update the initialization block in index.html with your credentials.
3.  In your Supabase dashboard, go to **Authentication -> Providers -> Email** and disable Confirm email.
4.  Create a Storage Bucket named pdfs.
5.  Run the following SQL to secure your bucket:
    `sql
    CREATE POLICY Allow users to manage their own files ON storage.objects
    FOR ALL TO authenticated
    USING (bucket_id = pdfs AND auth.uid() = owner)
    WITH CHECK (bucket_id = pdfs AND auth.uid() = owner);
    `

---
*Built with love for musicians.*