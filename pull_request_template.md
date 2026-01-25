# Pull request template
> [!IMPORTANT]
> Please complete all fields. PRs will not be merged if any fields are incomplete. Be respectful, and keep in mind that it may take some time for your PR to be reviewed.
>
> Bear in mind refactors are up to the developers and not it's contributors after all we are the ones giving support when needed. if they are big changes I suggest you to release it under your name instead.

## Type of change

- [x] Bug fix (non-breaking change which fixes an issue)
- [ ] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] This change requires a documentation update

### Motive for This Pull Request
Fixes critical issues where character appearance (makeup, hair colors) would not save or load correctly, and shop prices would not update for color-only changes.

### Provide a brief explanation of why these changes are being proposed and what they aim to achieve.
1. **Color Saving/Loading**: The script was storing palette hashes but character initialization functions were passing them directly to natives expecting indices. I implemented a hash-to-index translation in `FaceOverlay` and `ApplyOverlay` to bridge this gap.
2. **Shop Logic**: Changing only a color or opacity in the Barber/Makeup menus now correctly updates the total price, ensuring the save event is triggered.
3. **Data Structure**: Fixed several points where `Config.color_palettes` was incorrectly indexed as a list instead of a dictionary.

### Explain the necessity of these changes and how they will impact the framework or its users.
These fixes remove the common bug where players had to reload their character to see saved colors. It improves reliability for character customization and ensures server shops correctly charge players for all changes.

### Please describe the tests you have conducted to verify your changes. Provide instructions so we can reproduce these tests. Also, list any relevant details for your test configuration.
- [x] Tested with latest vorp scripts
- [x] Tested with latest artifacts
- Verified color persistence after relogging.
- Verified that changing ONLY a hair color at the barber shop results in a non-zero price and a successful database save.

## Notes if any
The hash-to-index translation logic ensures backward compatibility with existing databases that already contain HEX hashes instead of indices.
