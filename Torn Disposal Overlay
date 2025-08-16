// ==UserScript==
// @name         Torn Disposal Overlay
// @namespace    https://github.com/MK07/Torn-Disposal-Overlay
// @version      1.0.0
// @description  Displays disposal recommendations overlay on Torn's disposal page
// @author       MK07
// @homepage     https://github.com/MK07/Torn-Disposal-Overlay
// @supportURL   https://github.com/MK07/Torn-Disposal-Overlay/issues
// @match        https://www.torn.com/loader.php?sid=crimes*
// @match        https://www.torn.com/page.php?sid=crimes*
// @icon         https://raw.githubusercontent.com/MK07/Torn-Disposal-Overlay/main/Disposal%20Recommendation.png
// @grant        none
// @license      MIT
// ==/UserScript==

(function() {
    'use strict';
    
    // Prevent multiple instances
    if (window.tornDisposalOverlayActive) {
        console.log('[Torn Disposal Overlay] Already loaded');
        return;
    }
    window.tornDisposalOverlayActive = true;
    
    // Configuration
    const CONFIG = {
        imageUrl: 'https://raw.githubusercontent.com/MK07/Torn-Disposal-Overlay/main/Disposal%20Recommendation.png',
        position: { bottom: '20px', left: '20px' },
        size: { width: '300px', height: 'auto' },
        opacity: 0.8,
        zIndex: 9999
    };
    
    const OVERLAY_ID = 'torn-disposal-overlay';
    const OVERLAY_SELECTOR = `#${OVERLAY_ID}, [data-overlay="torn-disposal"]`;
    
    /**
     * Creates and displays the disposal overlay
     */
    function showOverlay() {
        // Remove any existing overlays
        hideOverlay();
        
        const overlay = document.createElement('img');
        overlay.id = OVERLAY_ID;
        overlay.src = CONFIG.imageUrl;
        overlay.alt = 'Disposal Recommendations';
        overlay.setAttribute('data-overlay', 'torn-disposal');
        
        // Apply styling
        Object.assign(overlay.style, {
            position: 'fixed',
            bottom: CONFIG.position.bottom,
            left: CONFIG.position.left,
            width: CONFIG.size.width,
            height: CONFIG.size.height,
            opacity: CONFIG.opacity,
            zIndex: CONFIG.zIndex,
            pointerEvents: 'none',
            borderRadius: '8px',
            boxShadow: '0 4px 12px rgba(0,0,0,0.3)',
            transition: 'opacity 0.3s ease-in-out'
        });
        
        // Add to page
        document.body.appendChild(overlay);
        console.log('[Torn Disposal Overlay] Overlay displayed');
    }
    
    /**
     * Removes the disposal overlay
     */
    function hideOverlay() {
        document.querySelectorAll(OVERLAY_SELECTOR).forEach(element => {
            element.remove();
        });
    }
    
    /**
     * Checks current page and shows/hides overlay accordingly
     */
    function updateOverlay() {
        const isDisposalPage = window.location.hash.startsWith('#/disposal');
        
        if (isDisposalPage) {
            showOverlay();
        } else {
            hideOverlay();
        }
    }
    
    /**
     * Initialize the overlay system
     */
    function initialize() {
        console.log('[Torn Disposal Overlay] Initializing...');
        
        // Initial check (delayed for SPA navigation)
        setTimeout(updateOverlay, 500);
        
        // Listen for navigation changes
        window.addEventListener('hashchange', updateOverlay, false);
        
        // Backup hash watcher for SPA edge cases
        let currentHash = window.location.hash;
        setInterval(() => {
            if (window.location.hash !== currentHash) {
                currentHash = window.location.hash;
                updateOverlay();
            }
        }, 1000);
        
        console.log('[Torn Disposal Overlay] Ready');
    }
    
    // Start the script
    initialize();
    
})();
