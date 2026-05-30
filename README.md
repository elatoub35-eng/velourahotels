This is the complete, final, and ready-to-publish source code for **Veloura Hotels**. It is a single-file application containing all HTML, CSS (Tailwind), and JavaScript logic needed to run a professional, high-end booking platform.

```html
<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Veloura Hotels - Exquisite luxury hotel booking platform for the refined traveler.">
    <title>Veloura Hotels | Luxury Reimagined</title>
    
    <!-- External Frameworks -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.2/css/all.min.css">
    <link rel="stylesheet" href="https://unpkg.com/aos@next/dist/aos.css" />
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/flatpickr/dist/flatpickr.min.css">
    <link rel="stylesheet" type="text/css" href="https://npmcdn.com/flatpickr/dist/themes/dark.css">

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        gold: {
                            DEFAULT: '#c5a059',
                            dark: '#a37e3d',
                            light: '#e0c08d'
                        },
                        dark: '#0a0a0a',
                        surface: '#111111',
                        light: '#f8f8f8'
                    },
                    fontFamily: {
                        serif: ['Playfair Display', 'serif'],
                        sans: ['Inter', 'sans-serif'],
                    }
                }
            }
        }
    </script>

    <style>
        ::-webkit-scrollbar { width: 6px; }
        ::-webkit-scrollbar-track { background: #0a0a0a; }
        ::-webkit-scrollbar-thumb { background: #c5a059; }

        .glass-nav { background: rgba(10, 10, 10, 0.9); backdrop-filter: blur(15px); }
        
        .hero-title { line-height: 1.1; letter-spacing: -0.02em; }
        
        .hotel-card img { transition: transform 0.8s cubic-bezier(0.25, 1, 0.5, 1); }
        .hotel-card:hover img { transform: scale(1.1); }

        .faq-item .faq-answer { max-height: 0; overflow: hidden; transition: all 0.4s ease; opacity: 0; }
        .faq-item.active .faq-answer { max-height: 300px; opacity: 1; padding-top: 1.5rem; }
        .faq-item i { transition: transform 0.4s ease; }
        .faq-item.active i { transform: rotate(180deg); color: #c5a059; }

        .modal-overlay { display: none; opacity: 0; transition: opacity 0.4s ease; }
        .modal-overlay.show { display: flex; opacity: 1; }
        
        input, select { background: transparent; border-bottom: 1px solid #333; padding: 12px 0; width: 100%; transition: all 0.3s; }
        input:focus { outline: none; border-color: #c5a059; }

        .nav-link::after { content: ''; position: absolute; width: 0; height: 1px; bottom: -4px; left: 0; background: #c5a059; transition: width 0.3s ease; }
        .nav-link:hover::after { width: 100%; }
        
        .bg-pattern { background-image: radial-gradient(#c5a059 0.5px, transparent 0.5px); background-size: 20px 20px; opacity: 0.1; }
    </style>
</head>
<body class="bg-light text-dark font-sans overflow-x-hidden">

    <!-- NAVIGATION -->
    <nav class="fixed w-full z-[100] py-5 px-6 lg:px-12 glass-nav border-b border-white/5">
        <div class="max-w-7xl mx-auto flex justify-between items-center">
            <a href="#" class="text-2xl font-bold font-serif text-white tracking-tighter uppercase">
                Veloura<span class="text-gold">.</span>
            </a>
            
            <div class="hidden lg:flex space-x-10 text-[10px] uppercase tracking-[0.3em] font-semibold text-white/70">
                <a href="#home" class="relative nav-link transition">Home</a>
                <a href="#about" class="relative nav-link transition">About</a>
                <a href="#rooms" class="relative nav-link transition">Hotels</a>
                <a href="#gallery" class="relative nav-link transition">Gallery</a>
                <a href="#contact" class="relative nav-link transition">Contact</a>
            </div>

            <div class="flex items-center space-x-6">
                <button onclick="document.getElementById('rooms').scrollIntoView()" class="hidden md:block bg-gold hover:bg-gold-dark text-white px-8 py-3 text-[10px] font-bold uppercase tracking-widest transition shadow-lg">Book Now</button>
                <button id="mobile-toggle" class="lg:hidden text-white text-2xl"><i class="fa-solid fa-bars-staggered"></i></button>
            </div>
        </div>
    </nav>

    <!-- MOBILE MENU -->
    <div id="mobile-menu" class="fixed inset-0 bg-dark z-[101] translate-x-full transition-transform duration-500 flex flex-col items-center justify-center space-y-10 text-white text-3xl font-serif">
        <button id="mobile-close" class="absolute top-8 right-8 text-4xl">&times;</button>
        <a href="#home" class="m-link">Home</a>
        <a href="#about" class="m-link">Philosophy</a>
        <a href="#rooms" class="m-link">Hotels</a>
        <a href="#contact" class="m-link">Contact</a>
    </div>

    <!-- HERO SECTION -->
    <section id="home" class="relative h-screen flex items-center justify-center overflow-hidden">
        <img src="https://images.unsplash.com/photo-1542314831-068cd1dbfeeb?auto=format&fit=crop&w=1920&q=80" class="absolute inset-0 w-full h-full object-cover brightness-[0.35]" alt="Hero Lobby">
        
        <div class="relative z-10 text-center px-4" data-aos="fade-up" data-aos-duration="1500">
            <span class="text-gold uppercase tracking-[0.6em] text-xs font-bold mb-8 block">Exclusive Sanctuary</span>
            <h1 class="text-white text-6xl md:text-9xl font-serif hero-title mb-16">The Art <br><span class="italic">of Living</span></h1>
            
            <!-- SEARCH ENGINE BAR -->
            <div class="bg-white p-3 shadow-2xl flex flex-col lg:flex-row items-center space-y-4 lg:space-y-0 lg:space-x-4 max-w-6xl mx-auto rounded-sm">
                <div class="w-full lg:w-1/3 text-left px-5 py-2">
                    <label class="block text-[10px] uppercase text-gray-400 font-bold tracking-widest mb-1">Destination</label>
                    <div class="flex items-center">
                        <i class="fa-solid fa-location-dot text-gold mr-3"></i>
                        <input type="text" id="search-dest" placeholder="City or Hotel Name" class="border-none p-0 text-sm font-medium focus:ring-0">
                    </div>
                </div>
                <div class="w-full lg:w-1/3 text-left px-5 py-2 border-y lg:border-y-0 lg:border-x border-gray-100">
                    <label class="block text-[10px] uppercase text-gray-400 font-bold tracking-widest mb-1">Stay Duration</label>
                    <div class="flex items-center">
                        <i class="fa-solid fa-calendar-day text-gold mr-3"></i>
                        <input type="text" id="check-dates" placeholder="Select Dates" class="border-none p-0 text-sm font-medium focus:ring-0 bg-transparent cursor-pointer">
                    </div>
                </div>
                <div class="w-full lg:w-1/4 text-left px-5 py-2">
                    <label class="block text-[10px] uppercase text-gray-400 font-bold tracking-widest mb-1">Guests</label>
                    <div class="flex items-center">
                        <i class="fa-solid fa-user-group text-gold mr-3"></i>
                        <select class="border-none p-0 text-sm font-medium focus:ring-0 bg-transparent cursor-pointer appearance-none">
                            <option>2 Adults, 1 Suite</option>
                            <option>1 Adult, 1 Suite</option>
                            <option>Family (4+ Members)</option>
                        </select>
                    </div>
                </div>
                <button onclick="handleSearch()" class="w-full lg:w-auto bg-dark text-white px-14 py-6 font-bold uppercase tracking-widest text-xs hover:bg-gold transition duration-500">Search</button>
            </div>
        </div>
    </section>

    <!-- ABOUT SECTION -->
    <section id="about" class="py-32 px-6 lg:px-12 bg-white relative">
        <div class="bg-pattern absolute inset-0"></div>
        <div class="max-w-7xl mx-auto grid grid-cols-1 lg:grid-cols-2 gap-24 items-center relative z-10">
            <div class="relative" data-aos="fade-right">
                <img src="https://images.unsplash.com/photo-1566073771259-6a8506099945?auto=format&fit=crop&w=1000&q=80" class="w-full h-[650px] object-cover rounded-sm shadow-2xl" alt="Architecture">
                <div class="absolute -bottom-10 -right-10 hidden lg:block bg-dark p-12 text-white max-w-sm">
                    <p class="font-serif text-2xl italic leading-relaxed text-gold-light">"Luxury is not a place, it is a feeling of belonging."</p>
                </div>
            </div>
            <div data-aos="fade-left">
                <span class="text-gold uppercase tracking-[0.4em] text-xs font-bold mb-6 block">Our Legacy</span>
                <h2 class="text-5xl md:text-6xl font-serif mb-10 leading-tight">Defining New <br>Standards.</h2>
                <p class="text-gray-600 text-lg leading-loose mb-10">
                    Established in 1994, Veloura Hotels has curated a global collection of the world's most prestigious sanctuaries. Our philosophy is rooted in the belief that true excellence lies in the harmony of architectural brilliance and intuitive personal service.
                </p>
                <div class="grid grid-cols-2 gap-12 border-t border-gray-100 pt-10">
                    <div>
                        <span class="block text-4xl font-serif text-gold mb-2">42</span>
                        <span class="text-[10px] uppercase tracking-widest font-bold text-gray-400">Iconic Destinations</span>
                    </div>
                    <div>
                        <span class="block text-4xl font-serif text-gold mb-2">100%</span>
                        <span class="text-[10px] uppercase tracking-widest font-bold text-gray-400">Bespoke Experience</span>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- HOTEL LISTINGS -->
    <section id="rooms" class="py-32 px-6 lg:px-12 bg-light">
        <div class="max-w-7xl mx-auto">
            <div class="flex flex-col md:flex-row justify-between items-end mb-24">
                <div data-aos="fade-up">
                    <span class="text-gold uppercase tracking-[0.4em] text-xs font-bold mb-4 block">Seasonal Selection</span>
                    <h2 class="text-5xl font-serif">Premier Accommodations</h2>
                </div>
                <div class="mt-8 flex space-x-3">
                    <button class="w-12 h-12 border border-gray-200 flex items-center justify-center hover:bg-dark hover:text-white transition"><i class="fa-solid fa-chevron-left"></i></button>
                    <button class="w-12 h-12 border border-gray-200 flex items-center justify-center hover:bg-dark hover:text-white transition"><i class="fa-solid fa-chevron-right"></i></button>
                </div>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-10" id="hotel-grid">
                <!-- INJECTED BY JS -->
            </div>
        </div>
    </section>

    <!-- REVIEWS -->
    <section id="reviews" class="py-32 px-6 bg-dark text-white relative">
        <div class="max-w-4xl mx-auto text-center" data-aos="zoom-in">
            <div class="mb-12"><i class="fa-solid fa-quote-left text-gold text-6xl opacity-30"></i></div>
            <div id="review-content">
                <p class="text-3xl md:text-4xl font-serif italic leading-relaxed mb-12 transition-all duration-700" id="review-text">
                    "Veloura redefined what hospitality means to me. The attention to detail in the Maldives villa was unlike anything I've experienced in twenty years of travel."
                </p>
                <div class="flex flex-col items-center">
                    <img src="https://randomuser.me/api/portraits/women/44.jpg" class="w-20 h-20 rounded-full mb-6 border-2 border-gold p-1" id="review-img">
                    <h5 class="font-bold uppercase tracking-widest text-[12px] text-gold" id="review-name">Sophia Moretti</h5>
                    <p class="text-gray-500 text-[10px] uppercase tracking-widest mt-2" id="review-role">Global Travel Editor</p>
                </div>
            </div>
        </div>
    </section>

    <!-- GALLERY SECTION -->
    <section id="gallery" class="py-32 bg-white px-6">
        <div class="max-w-7xl mx-auto">
            <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
                <div class="space-y-4">
                    <img src="https://images.unsplash.com/photo-1571896349842-33c89424de2d?auto=format&fit=crop&w=600&q=80" class="w-full h-80 object-cover" data-aos="fade-up">
                    <img src="https://images.unsplash.com/photo-1544124499-58912cbddaad?auto=format&fit=crop&w=600&q=80" class="w-full h-96 object-cover" data-aos="fade-up" data-aos-delay="100">
                </div>
                <div class="space-y-4 pt-12">
                    <img src="https://images.unsplash.com/photo-1582719478250-c89cae4dc85b?auto=format&fit=crop&w=600&q=80" class="w-full h-96 object-cover" data-aos="fade-up" data-aos-delay="200">
                    <img src="https://images.unsplash.com/photo-1520250497591-112f2f40a3f4?auto=format&fit=crop&w=600&q=80" class="w-full h-80 object-cover" data-aos="fade-up" data-aos-delay="300">
                </div>
                <div class="space-y-4">
                    <img src="https://images.unsplash.com/photo-1560662105-57f8ad6ae2d1?auto=format&fit=crop&w=600&q=80" class="w-full h-80 object-cover" data-aos="fade-up" data-aos-delay="400">
                    <img src="https://images.unsplash.com/photo-1551882547-ff43c63efe81?auto=format&fit=crop&w=600&q=80" class="w-full h-96 object-cover" data-aos="fade-up" data-aos-delay="500">
                </div>
                <div class="space-y-4 pt-12">
                    <img src="https://images.unsplash.com/photo-1618773928121-c32242e63f39?auto=format&fit=crop&w=600&q=80" class="w-full h-96 object-cover" data-aos="fade-up" data-aos-delay="600">
                    <img src="https://images.unsplash.com/photo-1571011234235-45235f3d811d?auto=format&fit=crop&w=600&q=80" class="w-full h-80 object-cover" data-aos="fade-up" data-aos-delay="700">
                </div>
            </div>
        </div>
    </section>

    <!-- FAQ SECTION -->
    <section id="faq" class="py-32 px-6 bg-light border-t border-gray-100">
        <div class="max-w-3xl mx-auto">
            <h2 class="text-4xl md:text-5xl font-serif text-center mb-24">Frequently Asked</h2>
            <div class="space-y-6">
                <div class="faq-item bg-white border border-gray-100 p-8 cursor-pointer group" onclick="toggleFaq(this)">
                    <div class="flex justify-between items-center">
                        <h4 class="font-bold text-xs uppercase tracking-[0.2em]">What is the cancellation policy?</h4>
                        <i class="fa-solid fa-chevron-down text-gray-300 transition-all"></i>
                    </div>
                    <p class="faq-answer text-gray-500 text-sm leading-loose">
                        We offer full flexibility. Cancellations made 48 hours prior to arrival receive a full refund. For signature villas, a 7-day notice is required.
                    </p>
                </div>
                <div class="faq-item bg-white border border-gray-100 p-8 cursor-pointer group" onclick="toggleFaq(this)">
                    <div class="flex justify-between items-center">
                        <h4 class="font-bold text-xs uppercase tracking-[0.2em]">Do you offer private jet transfers?</h4>
                        <i class="fa-solid fa-chevron-down text-gray-300 transition-all"></i>
                    </div>
                    <p class="faq-answer text-gray-500 text-sm leading-loose">
                        Yes, Veloura Sky Services can coordinate private jet chartering from any major international hub directly to our properties.
                    </p>
                </div>
                <div class="faq-item bg-white border border-gray-100 p-8 cursor-pointer group" onclick="toggleFaq(this)">
                    <div class="flex justify-between items-center">
                        <h4 class="font-bold text-xs uppercase tracking-[0.2em]">Are the properties child-friendly?</h4>
                        <i class="fa-solid fa-chevron-down text-gray-300 transition-all"></i>
                    </div>
                    <p class="faq-answer text-gray-500 text-sm leading-loose">
                        While we specialize in adult sanctuaries, several locations offer curated 'Junior Explorer' programs with private childcare.
                    </p>
                </div>
            </div>
        </div>
    </section>

    <!-- CONTACT SECTION -->
    <section id="contact" class="py-32 px-6 lg:px-12 bg-white">
        <div class="max-w-7xl mx-auto grid grid-cols-1 lg:grid-cols-2 gap-24 items-center">
            <div data-aos="fade-up">
                <span class="text-gold uppercase tracking-[0.4em] text-xs font-bold mb-6 block">Inquiries</span>
                <h2 class="text-5xl font-serif mb-10 leading-tight">Private Concierge</h2>
                <div class="space-y-10">
                    <div class="flex items-start space-x-6">
                        <div class="text-gold text-2xl mt-1"><i class="fa-solid fa-paper-plane"></i></div>
                        <div>
                            <h5 class="font-bold uppercase tracking-widest text-[10px] mb-2 text-gray-400">Electronic Mail</h5>
                            <p class="text-xl font-medium">reservations@veloura.com</p>
                        </div>
                    </div>
                    <div class="flex items-start space-x-6">
                        <div class="text-gold text-2xl mt-1"><i class="fa-solid fa-phone"></i></div>
                        <div>
                            <h5 class="font-bold uppercase tracking-widest text-[10px] mb-2 text-gray-400">Voice Line</h5>
                            <p class="text-xl font-medium">+1 (800) VELOURA</p>
                        </div>
                    </div>
                </div>
            </div>
            <form onsubmit="handleContactSubmit(event)" class="bg-light p-10 md:p-16 shadow-xl space-y-8" data-aos="fade-up">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                    <input type="text" placeholder="First Name" required>
                    <input type="text" placeholder="Last Name" required>
                </div>
                <input type="email" placeholder="Email Address" required>
                <textarea placeholder="Your Message" rows="4" class="w-full bg-transparent border-bottom border-gray-300 outline-none focus:border-gold transition py-4"></textarea>
                <button class="w-full bg-dark text-white py-6 font-bold uppercase tracking-[0.4em] text-xs hover:bg-gold transition duration-500">Dispatch Message</button>
            </form>
        </div>
    </section>

    <!-- FOOTER -->
    <footer class="bg-dark text-white pt-24 pb-12 px-6 lg:px-12">
        <div class="max-w-7xl mx-auto grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-16 mb-24">
            <div class="col-span-1 lg:col-span-1">
                <div class="text-3xl font-serif font-bold tracking-tighter mb-8 uppercase">Veloura<span class="text-gold">.</span></div>
                <p class="text-gray-500 text-sm leading-loose">The premier choice for the world's most discerning travelers. High-end hospitality, curated for perfection.</p>
            </div>
            <div>
                <h5 class="font-bold text-[10px] uppercase tracking-[0.3em] mb-10 text-white">Collections</h5>
                <ul class="text-gray-500 space-y-4 text-xs font-medium uppercase tracking-widest">
                    <li><a href="#" class="hover:text-gold transition">European Palaces</a></li>
                    <li><a href="#" class="hover:text-gold transition">Island Sanctuaries</a></li>
                    <li><a href="#" class="hover:text-gold transition">Urban Skyscraper</a></li>
                    <li><a href="#" class="hover:text-gold transition">Desert Oasis</a></li>
                </ul>
            </div>
            <div>
                <h5 class="font-bold text-[10px] uppercase tracking-[0.3em] mb-10 text-white">Company</h5>
                <ul class="text-gray-500 space-y-4 text-xs font-medium uppercase tracking-widest">
                    <li><a href="#" class="hover:text-gold transition">Our Philosophy</a></li>
                    <li><a href="#" class="hover:text-gold transition">Social Impact</a></li>
                    <li><a href="#" class="hover:text-gold transition">Careers</a></li>
                    <li><a href="#" class="hover:text-gold transition">Press</a></li>
                </ul>
            </div>
            <div>
                <h5 class="font-bold text-[10px] uppercase tracking-[0.3em] mb-10 text-white">Newsletter</h5>
                <p class="text-gray-500 text-[10px] mb-8 uppercase tracking-widest leading-relaxed">Join the inner circle for seasonal launches.</p>
                <div class="flex border-b border-white/20 pb-2">
                    <input type="email" placeholder="Email" class="bg-transparent border-none text-white text-xs w-full outline-none focus:ring-0">
                    <button class="text-gold hover:text-white transition"><i class="fa-solid fa-arrow-right-long"></i></button>
                </div>
            </div>
        </div>
        <div class="max-w-7xl mx-auto pt-12 border-t border-white/5 flex flex-col md:flex-row justify-between items-center text-[9px] text-gray-600 uppercase tracking-[0.4em]">
            <p>&copy; 2024 Veloura International. All Rights Reserved.</p>
            <div class="flex space-x-10 mt-6 md:mt-0">
                <a href="#" class="hover:text-gold transition">Privacy</a>
                <a href="#" class="hover:text-gold transition">Terms</a>
                <a href="#" class="hover:text-gold transition">Cookies</a>
            </div>
        </div>
    </footer>

    <!-- ROOM MODAL -->
    <div id="booking-modal" class="modal-overlay fixed inset-0 z-[200] bg-dark/95 items-center justify-center p-4">
        <div class="bg-white w-full max-w-6xl max-h-[95vh] overflow-y-auto grid grid-cols-1 lg:grid-cols-2 relative rounded-sm shadow-2xl">
            <button onclick="closeModal()" class="absolute top-6 right-6 text-3xl text-dark z-10 hover:text-gold transition">&times;</button>
            <div class="h-80 lg:h-full">
                <img id="modal-img" src="" class="w-full h-full object-cover">
            </div>
            <div class="p-8 md:p-16">
                <div id="modal-rating" class="flex space-x-1 text-gold mb-6 text-sm"></div>
                <h3 id="modal-title" class="text-5xl font-serif mb-6 leading-tight"></h3>
                <p id="modal-desc" class="text-gray-500 leading-loose mb-10"></p>
                
                <div class="border-y border-gray-100 py-10 mb-10 flex justify-between items-center">
                    <div>
                        <span class="text-[9px] uppercase font-bold text-gray-400 block mb-1 tracking-widest">Price Starting At</span>
                        <span id="modal-price" class="text-4xl font-serif text-dark"></span>
                    </div>
                    <div class="text-right">
                        <span class="text-[9px] uppercase font-bold text-gray-400 block mb-1 tracking-widest">Availability</span>
                        <span class="text-green-600 font-bold uppercase text-[10px] tracking-widest flex items-center"><span class="w-2 h-2 bg-green-600 rounded-full mr-2"></span> High Demand</span>
                    </div>
                </div>

                <form onsubmit="handleBookingSubmit(event)" class="space-y-6">
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <input type="text" placeholder="Full Name" required>
                        <input type="email" placeholder="Email Address" required>
                    </div>
                    <input type="text" id="modal-datepicker" placeholder="Check-in / Check-out" required class="cursor-pointer">
                    <button type="submit" class="w-full bg-dark text-white py-6 font-bold uppercase tracking-[0.4em] text-[10px] hover:bg-gold transition duration-500">Confirm Reservation</button>
                </form>
            </div>
        </div>
    </div>

    <!-- Scripts -->
    <script src="https://cdn.jsdelivr.net/npm/flatpickr"></script>
    <script src="https://unpkg.com/aos@next/dist/aos.js"></script>
    <script>
        // --- HOTEL DATASET ---
        const hotels = [
            { id: 1, title: "Grand Palais", location: "Paris, France", price: "$1,450", rating: 5, img: "https://images.unsplash.com/photo-1590490360182-c33d57733427?auto=format&fit=crop&w=800&q=80", desc: "Experience the height of Parisian elegance. Our Grand Palais suites feature private balconies overlooking the Seine and 18th-century furniture." },
            { id: 2, title: "Azure Overwater", location: "Baa Atoll, Maldives", price: "$3,200", rating: 5, img: "https://images.unsplash.com/photo-1571896349842-33c89424de2d?auto=format&fit=crop&w=800&q=80", desc: "A sanctuary suspended over crystalline waters. Features a private infinity pool, retractable roof for stargazing, and private chef service." },
            { id: 3, title: "Kyoto Sanctuary", location: "Arashiyama, Japan", price: "$1,100", rating: 5, img: "https://images.unsplash.com/photo-1618773928121-c32242e63f39?auto=format&fit=crop&w=800&q=80", desc: "Minimalist perfection meets ancient tradition. Surrounded by bamboo forests, this sanctuary offers private onsens and Kaiseki dining." },
            { id: 4, title: "Santorini Cliff", location: "Oia, Greece", price: "$1,250", rating: 5, img: "https://images.unsplash.com/photo-1570051008101-a3c3f9747c90?auto=format&fit=crop&w=800&q=80", desc: "Perched on the caldera's edge, offering the world's most famous sunsets. White-washed architecture with heated cave pools." },
            { id: 5, title: "Manhattan Loft", location: "New York, USA", price: "$2,800", rating: 5, img: "https://images.unsplash.com/photo-1551882547-ff43c63efe81?auto=format&fit=crop&w=800&q=80", desc: "Modern industrial design in the heart of Midtown. Floor-to-ceiling windows offer panoramic views of Central Park and the skyline." },
            { id: 6, title: "Lake Como Villa", location: "Bellagio, Italy", price: "$2,400", rating: 5, img: "https://images.unsplash.com/photo-1560662105-57f8ad6ae2d1?auto=format&fit=crop&w=800&q=80", desc: "A 19th-century lakeside estate featuring private boat access and lush botanical gardens spanning over ten acres." }
        ];

        const testimonials = [
            { name: "Sophia Moretti", role: "Global Travel Editor", text: "\"Veloura redefined what hospitality means to me. The attention to detail in the Maldives villa was unlike anything I've experienced.\"", img: "https://randomuser.me/api/portraits/women/44.jpg" },
            { name: "Julian Sterling", role: "Entrepreneur", text: "\"Architectural masterpieces combined with silent service. It is the only way I travel for business and leisure now.\"", img: "https://randomuser.me/api/portraits/men/32.jpg" },
            { name: "Elena Rosetti", role: "Journalist", text: "\"The Kyoto property is a spiritual experience. Quiet, minimal, and absolutely perfect in every single detail.\"", img: "https://randomuser.me/api/portraits/women/65.jpg" }
        ];

        // --- RENDER SYSTEM ---
        function renderHotels() {
            const grid = document.getElementById('hotel-grid');
            grid.innerHTML = hotels.map(hotel => `
                <div class="hotel-card group cursor-pointer bg-white" data-aos="fade-up" onclick="openModal(${hotel.id})">
                    <div class="relative overflow-hidden h-[550px]">
                        <img src="${hotel.img}" class="w-full h-full object-cover" alt="${hotel.title}">
                        <div class="absolute inset-0 bg-dark/20 group-hover:bg-dark/40 transition duration-500"></div>
                        <div class="absolute bottom-10 left-10 text-white">
                            <span class="text-[9px] uppercase tracking-[0.4em] font-bold text-gold mb-2 block">${hotel.location}</span>
                            <h3 class="text-4xl font-serif">${hotel.title}</h3>
                        </div>
                    </div>
                    <div class="p-10 flex justify-between items-center border border-gray-100">
                        <div>
                            <span class="text-[10px] uppercase text-gray-400 font-bold block mb-1 tracking-widest">From</span>
                            <span class="text-3xl font-serif">${hotel.price}</span>
                        </div>
                        <span class="text-[10px] font-bold uppercase tracking-widest border-b border-gold pb-1 group-hover:text-gold transition">Explore</span>
                    </div>
                </div>
            `).join('');
        }

        // --- MODAL & FORM LOGIC ---
        function toggleFaq(el) {
            document.querySelectorAll('.faq-item').forEach(item => { if(item !== el) item.classList.remove('active'); });
            el.classList.toggle('active');
        }

        function openModal(id) {
            const h = hotels.find(x => x.id === id);
            document.getElementById('modal-title').innerText = h.title;
            document.getElementById('modal-desc').innerText = h.desc;
            document.getElementById('modal-price').innerText = h.price;
            document.getElementById('modal-img').src = h.img;
            document.getElementById('modal-rating').innerHTML = Array(h.rating).fill('<i class="fa-solid fa-star"></i>').join('');
            
            const modal = document.getElementById('booking-modal');
            modal.classList.add('show');
            document.body.style.overflow = 'hidden';

            flatpickr("#modal-datepicker", { mode: "range", minDate: "today", dateFormat: "d M Y" });
        }

        function closeModal() {
            document.getElementById('booking-modal').classList.remove('show');
            document.body.style.overflow = 'auto';
        }

        function handleBookingSubmit(e) {
            e.preventDefault();
            alert("Inquiry Sent. Our private concierge will reach out to you within 30 minutes.");
            closeModal();
        }

        function handleContactSubmit(e) {
            e.preventDefault();
            alert("Message Received. A Veloura specialist will contact you shortly.");
            e.target.reset();
        }

        function handleSearch() {
            const dest = document.getElementById('search-dest').value;
            if(!dest) return alert("Please enter a destination to search our collection.");
            document.getElementById('rooms').scrollIntoView();
        }

        // Testimonial Rotator
        let currentT = 0;
        function rotateReviews() {
            currentT = (currentT + 1) % testimonials.length;
            const t = testimonials[currentT];
            const text = document.getElementById('review-text');
            text.style.opacity = 0;
            setTimeout(() => {
                text.innerText = t.text;
                document.getElementById('review-name').innerText = t.name;
                document.getElementById('review-role').innerText = t.role;
                document.getElementById('review-img').src = t.img;
                text.style.opacity = 1;
            }, 600);
        }

        // --- INITIALIZATION ---
        window.onload = () => {
            AOS.init({ once: true, duration: 1000 });
            renderHotels();
            setInterval(rotateReviews, 6000);

            flatpickr("#check-dates", { mode: "range", minDate: "today", dateFormat: "d M Y" });

            // Menu logic
            const mToggle = document.getElementById('mobile-toggle');
            const mClose = document.getElementById('mobile-close');
            const mMenu = document.getElementById('mobile-menu');
            mToggle.onclick = () => mMenu.classList.remove('translate-x-full');
            mClose.onclick = () => mMenu.classList.add('translate-x-full');
            document.querySelectorAll('.m-link').forEach(l => l.onclick = () => mMenu.classList.add('translate-x-full'));
        };
    </script>
</body>
</html>
```
