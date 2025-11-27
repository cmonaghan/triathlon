# Triathlon Results Analyzer

An interactive static website that allows you to analyze triathlon finish times and compare your performance against other athletes using bell curve distributions. Enter your name to see where your times fall within the distribution for swim, bike, run, and overall segments.

This uses the dataset from my most recent triathlon, which was publicly released by the race organizers here: https://my.raceresult.com/367536/

## Features

- **Athlete Search with Autocomplete**: Real-time autocomplete dropdown that updates as you type, with keyboard navigation (arrow keys and Enter)
- **Interactive Bell Curve Distributions**: Visualize where your times fall within the distribution for:
  - Swim time
  - Bike time
  - Run time
  - Overall finish time
- **Flexible Filtering**:
  - Filter by event (automatically set when athlete is selected)
  - Filter by gender (All, Male, Female, Agender)
  - Filter by age group (independent of gender - e.g., "25-29" includes both male and female athletes)
- **Real-time Updates**: All filters update immediately without requiring a button click
- **Percentile Rankings**: See your percentile ranking for each segment based on the filtered comparison group
- **Place Display**: Shows your place out of the total in the filtered group (e.g., "#11 of 19")

## Getting Started

### Prerequisites

- Python 3 (for local server) OR Vercel CLI (for deployment)
- A modern web browser

### Running Locally

1. **Start a local HTTP server** (required to load the CSV file):

   ```bash
   python3 -m http.server 8000
   ```

2. **Open in your browser**:

   Navigate to: `http://localhost:8000/triathlon_results_analyzer.html`

3. **Stop the server**:

   Press `Ctrl+C` in the terminal when you're done

### Deploying to Vercel

#### Option 1: Using Vercel CLI

1. **Install Vercel CLI** (if not already installed):

   ```bash
   npm i -g vercel
   ```

2. **Deploy**:

   ```bash
   vercel
   ```

3. **Follow the prompts** to link your project and deploy

#### Option 2: Using GitHub Integration

1. **Push your code to GitHub**

2. **Import project in Vercel**:
   - Go to [vercel.com](https://vercel.com)
   - Click "New Project"
   - Import your GitHub repository
   - Vercel will automatically detect it as a static site and deploy

3. **Your site will be live** at: `https://your-project.vercel.app/2025-napa`

The `vercel.json` configuration file routes `/2025-napa` to serve the main HTML file, keeping the URL clean.

## How to Use

1. **Enter an Athlete Name**:
   - Start typing an athlete's name in the search field
   - Use the autocomplete dropdown to select from matching names
   - Use arrow keys (↑/↓) to navigate suggestions
   - Press Enter to select a highlighted suggestion
   - The event dropdown will automatically be set and disabled

2. **Apply Filters** (optional):
   - **Gender Filter**: Select to compare against all genders, just your gender, or a specific gender
   - **Age Group Filter**: Select an age range to compare against (e.g., "25-29" includes both male and female athletes in that age range)
   - Filters update results immediately

3. **View Results**:
   - Athlete information card shows your details and overall place
   - Stat cards display your times and percentile rankings for each segment
   - Distribution charts show bell curves with your position highlighted in red
   - Percentile badges appear on chart titles when an athlete is selected

## File Structure

```
triathlon/
├── complete_triathlon_results.csv    # Triathlon results dataset
├── triathlon_results_analyzer.html   # Main application file
├── vercel.json                       # Vercel deployment configuration
└── README.md                         # This file
```

## Technical Details

- **Frontend**: React (via CDN), Chart.js for visualizations
- **Data Parsing**: PapaParse for CSV parsing
- **Styling**: Custom CSS with gradient designs
- **No Build Process**: The React code uses `React.createElement` calls directly (no JSX), so no transpilation is needed

## Data Format

The CSV file should contain the following columns:
- `Event`: The triathlon event name
- `Gender`: Athlete gender (Male, Female, Agender)
- `Age_Group`: Age group category (e.g., "Female 25-29", "Male 30-34")
- `Name`: Athlete name
- `Age`: Athlete age
- `Swim_Time`: Swim segment time (format: HH:MM:SS or MM:SS)
- `Bike_Time`: Bike segment time (format: HH:MM:SS or MM:SS)
- `Run_Time`: Run segment time (format: HH:MM:SS or MM:SS)
- `Finish_Time`: Overall finish time (format: HH:MM:SS or MM:SS)
- Additional columns: `Place`, `Bib`, `Club`, `Swim_Rank`, `Bike_Rank`, `Run_Rank`, etc.

## Features in Detail

### Age Group Filtering

The age group filter extracts just the age range from the dataset (e.g., "Female 25-29" → "25-29"), allowing you to:
- Compare athletes across genders within the same age range
- See how you rank against all athletes in your age group, regardless of gender
- Combine with gender filter for more specific comparisons

### Distribution Charts

- Each chart shows a histogram of times for the filtered group
- Your time is highlighted in red (`#f5576c`)
- Other athletes' times are shown in blue (`#667eea`)
- Charts update automatically when filters change
- Charts are visible even without an athlete selected (shows general distribution)

### Keyboard Navigation

- **Arrow Down**: Navigate down through autocomplete suggestions
- **Arrow Up**: Navigate up through autocomplete suggestions
- **Enter**: Select the highlighted suggestion
- **Escape**: Close the autocomplete dropdown

## Browser Compatibility

Works in all modern browsers that support:
- ES6 JavaScript features
- React 18
- Chart.js 4.4.0
- CSS Grid and Flexbox

## Notes

- The application uses an in-browser Babel transformer for development. For production, consider precompiling the React code.
- The CSV file must be served via HTTP (not file://) due to browser security restrictions.
- The application automatically handles time format conversions and calculates percentiles in real-time.

## License

This project is provided as-is for personal use.
