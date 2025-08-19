# Blog - Research Computing Group Jekyll Site

**ALWAYS FOLLOW THESE INSTRUCTIONS FIRST.** Only fall back to additional search and context gathering if the information in these instructions is incomplete or found to be in error.

This is a Jekyll-based static site blog for the Research Computing Group at Saint Louis University. The blog contains posts about digital humanities research, IIIF, transcription tools, and web annotation technologies from 2015-2024.

## Bootstrap, Build, and Run

### Dependencies
- Install Ruby (already available in most environments)
- Install Jekyll and required gems:
  ```bash
  sudo gem install jekyll bundler jekyll-feed jekyll-sitemap html-proofer
  ```
  - Takes 2-5 minutes to complete. NEVER CANCEL. Set timeout to 300+ seconds.

### Build Process
- **Build the site**: `jekyll build`
  - Builds in <1 second. Extremely fast.
  - Output goes to `_site/` directory
  - NEVER CANCEL builds - they complete almost immediately.

- **Verify build with verbose output**: `jekyll build --verbose`
  - Shows detailed processing of all posts and pages
  - Takes <1 second. Set timeout to 60+ seconds for safety.

### Development Server
- **Start development server**: `jekyll serve --host 0.0.0.0 --port 4000`
  - Server starts immediately and runs on http://localhost:4000
  - Includes live reload for content changes
  - NEVER CANCEL - server startup is immediate

- **Access the blog**: Navigate to http://localhost:4000 in browser
  - Blog loads immediately with all posts visible on homepage
  - Navigation works between "Blog" and "About" pages

## Validation and Quality Checks

### Jekyll Built-in Validation
- **Check configuration**: `jekyll doctor`
  - Validates _config.yml and identifies potential issues
  - Takes <1 second

### HTML Validation  
- **Basic HTML check**: `htmlproofer _site --disable-external --allow-hash-href`
  - Validates HTML structure and internal links
  - Takes <1 second. Set timeout to 60+ seconds for safety.
  - NOTE: Will show warnings about HTTP links and missing alt attributes - these are non-critical

- **Strict HTML validation**: `htmlproofer _site`
  - Includes external link checking (slower)
  - May fail on external HTTP links - this is expected

### Manual Validation Scenarios
**ALWAYS** test these scenarios after making changes:

1. **Home page loading**: Verify the blog homepage displays recent posts with excerpts
2. **Post navigation**: Click into individual posts and verify content renders correctly  
3. **About page**: Navigate to /about and verify page loads
4. **RSS feed**: Check that /feed.xml generates properly
5. **CSS/styling**: Verify site styling loads correctly (check style.css)

## Repository Structure

### Key Directories
- `_posts/`: Blog posts in Markdown format (32 posts from 2015-2024)
- `_layouts/`: HTML templates (default.html, post.html, page.html)  
- `_includes/`: Reusable template components (meta.html, analytics.html, etc.)
- `_sass/`: SCSS partials for styling
- `assets/images/`: Blog post images and assets
- `_site/`: Generated static site (created by build process)
- `attic/`: Older archived posts

### Key Files
- `_config.yml`: Jekyll configuration with site metadata
- `style.scss`: Main stylesheet that imports SASS partials
- `index.html`: Homepage template showing recent posts
- `about.md`: About page content

### Content Files
- Posts use YAML front matter with title, date, categories, tags
- Images referenced with `{{ site.baseurl }}/assets/images/` syntax
- Standard Jekyll/Liquid templating throughout

## Common Tasks

### Adding New Posts
1. Create new file in `_posts/` with format: `YYYY-MM-DD-title.md`
2. Add YAML front matter:
   ```yaml
   ---
   title: "Post Title"
   date: "YYYY-MM-DD"
   categories: 
     - "category"
   tags:
     - "tag1"
     - "tag2"
   author: "Author Name"
   ---
   ```
3. Write content in Markdown
4. Build and test: `jekyll build && jekyll serve`

### Updating Styling
1. Edit SCSS files in `_sass/` directory or `style.scss`
2. Jekyll automatically compiles SASS to CSS on build
3. Changes appear immediately in development server

### Working with Images
- Place images in `assets/images/`
- Reference in posts: `![alt text]({{ site.baseurl }}/assets/images/filename.jpg)`
- Jekyll processes and copies to `_site/assets/images/`

## Troubleshooting

### Common Issues
- **"Liquid syntax error"**: Check for unescaped curly braces in post content
- **Images not loading**: Verify image paths use `{{ site.baseurl }}/assets/images/`
- **Styling missing**: Ensure `style.scss` compiles correctly with `jekyll build`

### Debug Commands
- `jekyll build --trace`: Shows full error backtraces
- `jekyll serve --verbose`: Detailed server startup info  
- `jekyll doctor`: Validates configuration

## Performance Notes
- All builds complete in <1 second due to small site size
- Development server starts immediately  
- HTML validation runs in <1 second
- Site generation is extremely fast - no performance concerns

## What NOT to do
- Do not run builds with short timeouts - use 60+ seconds minimum for safety
- Do not install additional build tools - Jekyll handles everything
- Do not modify the _site directory directly - it gets regenerated on each build
- Do not commit _site directory - it's excluded in .gitignore

## Testing New Changes
1. Always run `jekyll build` after making changes
2. Start development server: `jekyll serve --host 0.0.0.0 --port 4000`  
3. Test the homepage and navigate through the blog
4. Verify new/modified content displays correctly
5. Run HTML validation: `htmlproofer _site --disable-external --allow-hash-href`
6. Check for any broken internal links or formatting issues