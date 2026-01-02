# Browser Automation Rules

## Critical Rules

1. **NEVER trust claims - verify with screenshots**
   After any browser action, IMMEDIATELY verify the screenshot BEFORE reporting success.

2. **Check state before AND after**
   - Take screenshot before starting
   - Take screenshot after each major action
   - Compare to verify changes happened

3. **Handle loading states**
   - If page looks like it's loading, wait and take another screenshot
   - Don't assume content is ready
   - Check for loading spinners, skeleton screens

4. **Verify element positions**
   - Think about whether elements appear where expected
   - If not, check current screenshot and DOM

## Screenshot Rules

- Do NOT view .webp recordings (only shows first frame)
- Rely on PNG/JPEG screenshots only
- If no screenshots exist, take them to prove completion

## Console Errors

- ALWAYS check browser console for errors
- Report any JavaScript errors, warnings, or failed network requests
- Console errors may indicate the page didn't load correctly

## Verification Checklist

Before reporting success:
- [ ] Screenshot shows expected result
- [ ] No console errors
- [ ] All interactive elements are visible
- [ ] Page is fully loaded (no spinners)
- [ ] URLs match expected values

## Error Handling

If verification fails:
1. Take new screenshot
2. Check console logs
3. Report what actually happened vs expected
4. Suggest next steps
