# Codebase Cleanup & UI Fixes Plan

## Project Analysis Summary

**Tech Stack Detected:** Plain HTML/CSS/JavaScript (not React/Next.js)
- **HTML:** Single-page application with multiple sections
- **CSS:** Large CSS files with potential unused styles
- **JavaScript:** Multiple JS files with some potential dead code
- **Translation System:** Recently implemented with some issues

## Critical Issues Identified

### 1. **Hero Section Button Issues** 🚨 HIGH PRIORITY
- **Missing `openQuiz()` function** - Second button calls undefined function
- **Potential z-index/overlay issues** - Need to verify clickable areas
- **Responsive design concerns** - Buttons may not work properly on mobile

### 2. **Translation System Issues**
- **Missing function definition** - `openQuiz()` not found in any JS file
- **Potential text overflow** - Longer French translations may break layout
- **RTL support incomplete** - Arabic translations exist but RTL styles may be insufficient

### 3. **Code Quality Issues**
- **Large CSS files** - `app.css` (8,872 lines), `app.min.css` (10,635 lines)
- **Potential unused styles** - No CSS purging implemented
- **Multiple JS files** - Some may contain dead code
- **No linting/formatting** - Code style inconsistencies

## Cleanup Strategy

### Phase 1: Critical UI Fixes (Immediate)

#### 1.1 Fix Hero Section Buttons
```javascript
// Add missing openQuiz function
function openQuiz() {
  // Show the quiz modal
  const modalOverlay = document.getElementById('modalOverlay');
  if (modalOverlay) {
    modalOverlay.style.display = 'flex';
  }
}
```

#### 1.2 Verify Button Accessibility
- [ ] Test keyboard navigation (Tab, Enter, Space)
- [ ] Verify focus states are visible
- [ ] Check ARIA labels and roles
- [ ] Test on all breakpoints (mobile, tablet, desktop)

#### 1.3 Fix Translation Text Overflow
- [ ] Add `overflow-wrap: break-word` for long translations
- [ ] Implement responsive text sizing
- [ ] Test with longest possible French text

### Phase 2: Code Cleanup

#### 2.1 CSS Optimization
**Files to analyze:**
- `assets/css/app.css` (8,872 lines)
- `assets/css/app.min.css` (10,635 lines)
- `assets/css/main.css` (1,088 lines)
- `assets/css/nvp-style.css` (458 lines)

**Actions:**
- [ ] Identify unused CSS classes
- [ ] Remove duplicate styles
- [ ] Consolidate media queries
- [ ] Implement CSS purging (PurgeCSS)

#### 2.2 JavaScript Cleanup
**Files to analyze:**
- `assets/js/app.js` (518 lines)
- `assets/js/website-translations.js` (547 lines)
- `assets/js/nvp-script.js` (364 lines)
- `assets/js/popup-quiz.js` (272 lines)

**Actions:**
- [ ] Remove unused functions
- [ ] Consolidate duplicate code
- [ ] Remove console.log statements
- [ ] Optimize event listeners

#### 2.3 Asset Cleanup
**Files to check:**
- [ ] Unused images in `assets/images/`
- [ ] Duplicate font files
- [ ] Unused JavaScript libraries

### Phase 3: Performance Optimization

#### 3.1 Bundle Optimization
- [ ] Minify CSS and JS files
- [ ] Optimize image sizes
- [ ] Implement lazy loading for images
- [ ] Add compression headers

#### 3.2 Code Splitting
- [ ] Separate critical CSS
- [ ] Load non-critical JS asynchronously
- [ ] Implement service worker for caching

## Implementation Plan

### Step 1: Create Safety Net
```bash
# Create backup branch
git checkout -b backup-before-cleanup
git add .
git commit -m "Backup before cleanup"

# Create working branch
git checkout -b fix/ui-cleanup
```

### Step 2: Fix Critical Issues First
1. **Add missing `openQuiz()` function**
2. **Test hero buttons on all devices**
3. **Fix translation overflow issues**
4. **Verify accessibility compliance**

### Step 3: Implement Tooling
```bash
# Add ESLint for JavaScript
npm init -y
npm install --save-dev eslint prettier

# Add CSS linting
npm install --save-dev stylelint stylelint-config-standard

# Add PurgeCSS for unused CSS removal
npm install --save-dev purgecss
```

### Step 4: Code Cleanup
1. **Run static analysis tools**
2. **Remove unused code**
3. **Optimize CSS**
4. **Clean up JavaScript**

### Step 5: Testing & Validation
1. **Cross-browser testing**
2. **Mobile responsiveness testing**
3. **Accessibility testing**
4. **Performance testing (Lighthouse)**

## Files Requiring Immediate Attention

### High Priority
1. **`index.html`** - Add missing `openQuiz()` function
2. **`assets/css/app.css`** - Optimize and remove unused styles
3. **`assets/js/website-translations.js`** - Fix translation issues

### Medium Priority
1. **`assets/js/app.js`** - Clean up and optimize
2. **`assets/js/nvp-script.js`** - Remove duplicates
3. **`assets/css/main.css`** - Consolidate with app.css

### Low Priority
1. **Image optimization** - Compress and resize
2. **Font optimization** - Remove unused font files
3. **Documentation** - Add code comments and README

## Success Metrics

### Performance Targets
- [ ] Lighthouse Performance Score: ≥85
- [ ] Lighthouse Accessibility Score: ≥90
- [ ] Lighthouse Best Practices Score: ≥90
- [ ] Lighthouse SEO Score: ≥90

### Code Quality Targets
- [ ] No ESLint errors
- [ ] No unused CSS classes
- [ ] No console.log statements in production
- [ ] All functions properly defined

### User Experience Targets
- [ ] Hero buttons work on all devices
- [ ] Translations display correctly
- [ ] No layout shifts during language switching
- [ ] All interactive elements are keyboard accessible

## Risk Mitigation

### Before Making Changes
1. **Create complete backup**
2. **Test on staging environment**
3. **Document current functionality**
4. **Plan rollback strategy**

### During Implementation
1. **Make small, atomic commits**
2. **Test after each change**
3. **Keep original files as backup**
4. **Monitor for regressions**

### After Implementation
1. **Comprehensive testing**
2. **Performance monitoring**
3. **User feedback collection**
4. **Documentation updates**

## Next Steps

1. **Start with Phase 1** - Fix critical hero button issues
2. **Implement basic tooling** - ESLint, Prettier, Stylelint
3. **Begin CSS optimization** - Remove unused styles
4. **Clean up JavaScript** - Remove dead code
5. **Performance optimization** - Minify and compress
6. **Final testing** - Cross-browser and accessibility testing

This plan ensures we fix the most critical issues first while systematically improving the overall codebase quality and performance.
