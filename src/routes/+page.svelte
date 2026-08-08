<script lang="ts">
	import { onMount } from 'svelte';
	import { base } from '$app/paths';

	const programs = [
		{
			number: '01',
			title: 'Plan your path',
			text: 'Clear, unbiased guidance to compare programs, scholarships, and countries with confidence.',
			color: 'sage'
		},
		{
			number: '02',
			title: 'Prepare to go',
			text: 'Practical support for applications, documents, visas, budgeting, and pre-departure.',
			color: 'sand'
		},
		{
			number: '03',
			title: 'Belong & thrive',
			text: 'Local mentors, peer circles, and resources for wellbeing, work, and life in a new place.',
			color: 'coral'
		}
	];

	const stories = [
		{
			quote:
				'My mentor helped me turn a confusing process into a clear plan. I arrived feeling prepared—not alone.',
			name: 'Nadia Rahman',
			detail: 'Bangladesh → Canada',
			image:
				'https://images.unsplash.com/photo-1494790108377-be9c29b29330?auto=format&fit=crop&w=240&q=85'
		},
		{
			quote:
				'Kawan connected me with students who understood exactly what I was going through.',
			name: 'Mateo Silva',
			detail: 'Brazil → Germany',
			image:
				'https://images.unsplash.com/photo-1500648767791-00dcc994a43e?auto=format&fit=crop&w=240&q=85'
		},
		{
			quote:
				'I found a scholarship I would never have discovered on my own. It changed what felt possible.',
			name: 'Amara Okafor',
			detail: 'Nigeria → United Kingdom',
			image:
				'https://images.unsplash.com/photo-1534528741775-53994a69daeb?auto=format&fit=crop&w=240&q=85'
		}
	];

	let menuOpen = false;
	let storyIndex = 0;
	let email = '';
	let submitted = false;

	function subscribe() {
		if (email.trim()) {
			submitted = true;
			email = '';
		}
	}

	onMount(() => {
		const observer = new IntersectionObserver(
			(entries) => {
				for (const entry of entries) {
					if (entry.isIntersecting) entry.target.classList.add('visible');
				}
			},
			{ threshold: 0.12 }
		);

		document.querySelectorAll('.reveal').forEach((element) => observer.observe(element));
		return () => observer.disconnect();
	});
</script>

<svelte:head>
	<title>Kawan — Your journey. Our guidance.</title>
</svelte:head>

<header class="site-header">
	<a class="brand" href="#top" aria-label="Kawan home">
		<span class="brand-mark" aria-hidden="true">
			<svg viewBox="0 0 44 44" fill="none">
				<path d="M5 27.5c7-12 16-15 33-12-7.5 2.8-11 8-12.2 15.2C20 24.8 13.2 24.5 5 27.5Z" fill="currentColor" />
				<path d="M10 32c8-5 15-5.8 24-3.2" stroke="currentColor" stroke-width="2.7" stroke-linecap="round" />
			</svg>
		</span>
		<span>Kawan</span>
	</a>

	<nav class:open={menuOpen} aria-label="Primary navigation">
		<a href="#about" onclick={() => (menuOpen = false)}>About</a>
		<a href="#programs" onclick={() => (menuOpen = false)}>How we help</a>
		<a href="#stories" onclick={() => (menuOpen = false)}>Stories</a>
		<a href="#resources" onclick={() => (menuOpen = false)}>Resources</a>
	</nav>

	<a class="button small desktop-cta" href="#connect">Get guidance <span>↗</span></a>
	<button
		class="menu-button"
		class:active={menuOpen}
		aria-label="Toggle navigation"
		aria-expanded={menuOpen}
		onclick={() => (menuOpen = !menuOpen)}
	>
		<span></span><span></span>
	</button>
</header>

<main id="top">
	<section class="hero">
		<div class="hero-grid">
			<div class="hero-copy reveal visible">
				<p class="eyebrow"><span></span> Guidance without borders</p>
				<h1>Your journey.<br /><em>Our guidance.</em></h1>
				<p class="hero-lead">
					Free, trusted support for international students—from the first big dream to feeling at
					home in a new country.
				</p>
				<div class="hero-actions">
					<a class="button" href="#connect">Start your journey <span>↗</span></a>
					<a class="text-link" href="#about">Discover our mission <span>↓</span></a>
				</div>
				<div class="trust-row">
					<div class="avatar-stack" aria-hidden="true">
						<img src="https://images.unsplash.com/photo-1524504388940-b1c1722653e1?auto=format&fit=crop&w=90&q=80" alt="" />
						<img src="https://images.unsplash.com/photo-1506794778202-cad84cf45f1d?auto=format&fit=crop&w=90&q=80" alt="" />
						<img src="https://images.unsplash.com/photo-1544005313-94ddf0286df2?auto=format&fit=crop&w=90&q=80" alt="" />
					</div>
					<p><strong>4,800+ students</strong><br />supported across 32 countries</p>
				</div>
			</div>

			<div class="hero-visual reveal visible">
				<div class="sun-shape"></div>
				<div class="photo-frame">
					<img
						src="https://images.unsplash.com/photo-1523240795612-9a054b0db644?auto=format&fit=crop&w=1200&q=88"
						alt="International students laughing together on campus"
					/>
				</div>
				<div class="route-card">
					<div class="route-icon">
						<svg viewBox="0 0 24 24" fill="none" aria-hidden="true">
							<path d="M3 11.5 21 4l-7.5 18-2.4-8.1L3 11.5Z" stroke="currentColor" stroke-width="1.8" stroke-linejoin="round" />
						</svg>
					</div>
					<div><span>Next stop</span><strong>Your future</strong></div>
				</div>
				<div class="destination-chip">32 countries <span>✦</span> one community</div>
			</div>
		</div>
		<div class="scroll-note"><span></span> SCROLL TO EXPLORE</div>
	</section>

	<section class="mission" id="about">
		<div class="section-wrap mission-grid">
			<div class="section-heading reveal">
				<p class="eyebrow light"><span></span> Why we exist</p>
				<h2>Big dreams shouldn't come with <em>impossible questions.</em></h2>
			</div>
			<div class="mission-copy reveal">
				<p>
					Studying abroad can transform a life—but the path there is often confusing, expensive,
					and lonely. We're here to change that.
				</p>
				<p>
					Kawan is a nonprofit powered by people who have made the journey themselves. We
					offer free, honest guidance so every student can move forward with clarity and courage.
				</p>
				<a class="inline-link" href="#programs">Read our story <span>↗</span></a>
			</div>
		</div>
		<div class="impact-strip reveal">
			<div><strong>4,800<span>+</span></strong><small>STUDENTS GUIDED</small></div>
			<div><strong>32</strong><small>COUNTRIES REACHED</small></div>
			<div><strong>380<span>+</span></strong><small>VOLUNTEER MENTORS</small></div>
			<div><strong>91<span>%</span></strong><small>FEEL MORE CONFIDENT</small></div>
		</div>
	</section>

	<section class="programs section-wrap" id="programs">
		<div class="programs-header reveal">
			<div>
				<p class="eyebrow"><span></span> How we help</p>
				<h2>Support for every<br /><em>step forward.</em></h2>
			</div>
			<p>
				Wherever you are in your journey, you'll find practical tools, trusted answers, and people
				who believe in you.
			</p>
		</div>

		<div class="program-grid">
			{#each programs as program, index}
				<article class="program-card {program.color} reveal" style={`--delay: ${index * 90}ms`}>
					<div class="card-top">
						<span>{program.number}</span>
						<div class="program-icon">
							{#if index === 0}
								<svg viewBox="0 0 40 40" fill="none" aria-hidden="true">
									<circle cx="20" cy="20" r="14" stroke="currentColor" stroke-width="1.8" />
									<path d="m15 25 3-8 8-3-3 8-8 3Z" stroke="currentColor" stroke-width="1.8" stroke-linejoin="round" />
									<circle cx="20.5" cy="19.5" r="1.4" fill="currentColor" />
								</svg>
							{:else if index === 1}
								<svg viewBox="0 0 40 40" fill="none" aria-hidden="true">
									<path d="M8 25.5h24M13 25.5v-11h14v11M10 30h20M17 14.5v-4h6v4" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" />
									<path d="M17 20h6" stroke="currentColor" stroke-width="1.8" />
								</svg>
							{:else}
								<svg viewBox="0 0 40 40" fill="none" aria-hidden="true">
									<path d="M20 31s-11-5.8-11-13.3A6.7 6.7 0 0 1 20 12.5a6.7 6.7 0 0 1 11 5.2C31 25.2 20 31 20 31Z" stroke="currentColor" stroke-width="1.8" />
									<path d="M15.5 20.5c1.3 1.2 2.8 1.8 4.5 1.8s3.2-.6 4.5-1.8" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" />
								</svg>
							{/if}
						</div>
					</div>
					<h3>{program.title}</h3>
					<p>{program.text}</p>
					<a href="#connect" aria-label={`Explore ${program.title}`}>Explore support <span>↗</span></a>
				</article>
			{/each}
		</div>
	</section>

	<section class="mentor-band" id="connect">
		<div class="mentor-image reveal">
			<img
				src="https://images.unsplash.com/photo-1522202176988-66273c2fd55f?auto=format&fit=crop&w=1100&q=86"
				alt="A student and mentor working together"
			/>
			<div class="availability"><span></span> 24 mentors available this week</div>
		</div>
		<div class="mentor-copy reveal">
			<p class="eyebrow light"><span></span> One-to-one support</p>
			<h2>Meet someone who's <em>been where you are.</em></h2>
			<p>
				Our volunteer mentors were international students too. Get matched with someone who knows
				your destination, speaks your language, and understands the questions on your mind.
			</p>
			<div class="mentor-points">
				<span>✓ Always free</span><span>✓ Thoughtfully matched</span><span>✓ On your schedule</span>
			</div>
			<a class="button gold" href="mailto:hello@kawan.org">Find your mentor <span>↗</span></a>
		</div>
	</section>

	<section class="stories section-wrap" id="stories">
		<div class="stories-intro reveal">
			<p class="eyebrow"><span></span> Student stories</p>
			<h2>Journeys that<br /><em>inspire ours.</em></h2>
			<div class="story-controls">
				<button aria-label="Previous story" onclick={() => (storyIndex = (storyIndex + stories.length - 1) % stories.length)}>←</button>
				<button aria-label="Next story" onclick={() => (storyIndex = (storyIndex + 1) % stories.length)}>→</button>
			</div>
		</div>
		<div class="story-card reveal">
			<div class="quote-mark">“</div>
			<blockquote>{stories[storyIndex].quote}</blockquote>
			<div class="student">
				<img src={stories[storyIndex].image} alt={stories[storyIndex].name} />
				<div><strong>{stories[storyIndex].name}</strong><span>{stories[storyIndex].detail}</span></div>
			</div>
			<div class="story-progress" aria-label={`Story ${storyIndex + 1} of ${stories.length}`}>
				{#each stories as _, index}
					<button class:active={index === storyIndex} onclick={() => (storyIndex = index)} aria-label={`Show story ${index + 1}`}></button>
				{/each}
			</div>
		</div>
	</section>

	<section class="resources" id="resources">
		<div class="section-wrap">
			<div class="resource-heading reveal">
				<div>
					<p class="eyebrow"><span></span> Free resources</p>
					<h2>Good guidance,<br /><em>within reach.</em></h2>
				</div>
				<a class="inline-link" href="#guide">View all resources <span>↗</span></a>
			</div>
			<div class="resource-grid" id="guide">
				<article class="feature-resource reveal">
					<div class="feature-art">
						<span class="art-stamp">2026<br />EDITION</span>
						<div class="book">
							<small>THE ESSENTIAL GUIDE</small>
							<strong>Your First<br />90 Days<br />Abroad</strong>
							<span>KAWAN</span>
						</div>
					</div>
					<div class="resource-content">
						<span class="tag">FEATURED GUIDE</span>
						<h3>Your First 90 Days Abroad</h3>
						<p>A practical guide to arriving, settling in, and building a life that feels like yours.</p>
						<a href={`${base}/guides/first-90-days.txt`} download>Download free guide <span>↓</span></a>
					</div>
				</article>
				<article class="mini-resource reveal">
					<div class="mini-icon">⌁</div>
					<span class="tag">CHECKLIST</span>
					<h3>The application<br />master checklist</h3>
					<a href="#connect">Open resource <span>↗</span></a>
				</article>
				<article class="mini-resource green reveal">
					<div class="mini-icon">◌</div>
					<span class="tag">TOOLKIT</span>
					<h3>Scholarship search<br />starter kit</h3>
					<a href="#connect">Open resource <span>↗</span></a>
				</article>
			</div>
		</div>
	</section>

	<section class="cta-section">
		<div class="cta-orbit one"></div>
		<div class="cta-orbit two"></div>
		<div class="cta-content reveal">
			<p class="eyebrow centered"><span></span> Your next chapter starts here <span></span></p>
			<h2>You don't have to figure<br />it out <em>alone.</em></h2>
			<p>Tell us where you are in your journey. We'll help you find your next clear step.</p>
			<div class="cta-actions">
				<a class="button gold" href="mailto:hello@kawan.org">Get free guidance <span>↗</span></a>
				<a href="mailto:volunteer@kawan.org">Become a volunteer <span>→</span></a>
			</div>
		</div>
	</section>
</main>

<footer>
	<div class="footer-main section-wrap">
		<div class="footer-brand">
			<a class="brand inverse" href="#top">
				<span class="brand-mark" aria-hidden="true">
					<svg viewBox="0 0 44 44" fill="none">
						<path d="M5 27.5c7-12 16-15 33-12-7.5 2.8-11 8-12.2 15.2C20 24.8 13.2 24.5 5 27.5Z" fill="currentColor" />
						<path d="M10 32c8-5 15-5.8 24-3.2" stroke="currentColor" stroke-width="2.7" stroke-linecap="round" />
					</svg>
				</span>
				<span>Kawan</span>
			</a>
			<p>Guidance without borders.<br />Opportunity without limits.</p>
			<div class="socials"><a href="#top">in</a><a href="#top">ig</a><a href="#top">yt</a></div>
		</div>
		<div class="footer-links">
			<div><strong>EXPLORE</strong><a href="#about">About us</a><a href="#programs">How we help</a><a href="#stories">Student stories</a><a href="#resources">Resources</a></div>
			<div><strong>GET INVOLVED</strong><a href="mailto:volunteer@kawan.org">Volunteer</a><a href="#connect">Partner with us</a><a href="#connect">Donate</a><a href="#connect">Careers</a></div>
		</div>
		<div class="newsletter">
			<strong>STAY IN THE LOOP</strong>
			<p>Stories, resources, and practical tips—once a month.</p>
			{#if submitted}
				<div class="thanks">Thank you — you're on the list!</div>
			{:else}
				<form onsubmit={(event) => { event.preventDefault(); subscribe(); }}>
					<label class="sr-only" for="email">Email address</label>
					<input id="email" type="email" required placeholder="Your email address" bind:value={email} />
					<button aria-label="Subscribe">→</button>
				</form>
			{/if}
		</div>
	</div>
	<div class="footer-bottom section-wrap">
		<span>© 2026 KAWAN. REGISTERED NONPROFIT.</span>
		<div><a href="#top">PRIVACY</a><a href="#top">TERMS</a><a href="#top">ACCESSIBILITY</a></div>
	</div>
</footer>

<style>
	:global(.reveal) {
		opacity: 0;
		transform: translateY(24px);
		transition: opacity 0.7s ease, transform 0.7s ease;
		transition-delay: var(--delay, 0ms);
	}

	:global(.reveal.visible) {
		opacity: 1;
		transform: translateY(0);
	}

	.site-header {
		position: absolute;
		z-index: 20;
		top: 0;
		left: 50%;
		display: flex;
		width: min(1280px, calc(100% - 64px));
		height: 96px;
		align-items: center;
		justify-content: space-between;
		transform: translateX(-50%);
	}

	.brand {
		display: inline-flex;
		align-items: center;
		font-family: 'Manrope', sans-serif;
		font-size: 21px;
		font-weight: 800;
		letter-spacing: -0.7px;
	}

	.brand > span:last-child > span {
		color: var(--gold);
	}

	.brand-mark {
		display: inline-flex;
		width: 42px;
		height: 42px;
		margin-right: 9px;
		color: var(--forest);
	}

	nav {
		display: flex;
		gap: 37px;
		margin-left: 90px;
	}

	nav a {
		position: relative;
		color: #294a43;
		font-size: 14px;
		font-weight: 600;
	}

	nav a::after {
		position: absolute;
		right: 0;
		bottom: -7px;
		left: 0;
		height: 2px;
		background: var(--gold);
		content: '';
		transform: scaleX(0);
		transition: transform 0.25s ease;
	}

	nav a:hover::after {
		transform: scaleX(1);
	}

	.button {
		display: inline-flex;
		min-height: 52px;
		align-items: center;
		justify-content: center;
		gap: 18px;
		padding: 0 25px;
		border-radius: 5px;
		color: #fff;
		background: var(--forest);
		box-shadow: 0 10px 25px rgba(20, 95, 82, 0.18);
		font-size: 14px;
		font-weight: 700;
		transition: transform 0.2s ease, background 0.2s ease;
	}

	.button:hover {
		background: var(--forest-dark);
		transform: translateY(-2px);
	}

	.button.small {
		min-height: 44px;
		padding: 0 19px;
	}

	.button.gold {
		color: var(--ink);
		background: var(--gold);
		box-shadow: none;
	}

	.button.gold:hover {
		background: #ffc979;
	}

	.menu-button {
		display: none;
		width: 44px;
		height: 44px;
		padding: 13px 10px;
		border-radius: 50%;
		background: var(--forest);
	}

	.menu-button span {
		display: block;
		width: 100%;
		height: 2px;
		margin: 5px 0;
		background: white;
		transition: transform 0.2s ease;
	}

	.hero {
		position: relative;
		min-height: 785px;
		overflow: hidden;
		background: linear-gradient(106deg, #f8f4e9 0 54%, #e3f0eb 54%);
	}

	.hero::before {
		position: absolute;
		top: -120px;
		left: -170px;
		width: 500px;
		height: 500px;
		border: 1px solid rgba(20, 95, 82, 0.08);
		border-radius: 50%;
		content: '';
	}

	.hero-grid {
		display: grid;
		width: min(1280px, calc(100% - 64px));
		min-height: 785px;
		margin: auto;
		grid-template-columns: 48% 52%;
		align-items: center;
	}

	.hero-copy {
		position: relative;
		z-index: 2;
		padding-top: 76px;
	}

	.eyebrow {
		display: flex;
		align-items: center;
		gap: 10px;
		margin-bottom: 26px;
		color: var(--forest);
		font-size: 11px;
		font-weight: 800;
		letter-spacing: 2.1px;
		text-transform: uppercase;
	}

	.eyebrow > span {
		width: 28px;
		height: 1px;
		background: var(--gold);
	}

	.eyebrow.light {
		color: #b5d8ce;
	}

	h1 {
		max-width: 690px;
		margin-bottom: 27px;
		color: var(--ink);
		font-size: clamp(62px, 6.3vw, 94px);
		font-weight: 700;
		line-height: 0.98;
		letter-spacing: -5.8px;
	}

	h1 em,
	h2 em {
		color: var(--forest);
		font-family: Georgia, serif;
		font-weight: 400;
	}

	.hero-lead {
		max-width: 505px;
		margin-bottom: 34px;
		color: var(--muted);
		font-size: 17px;
		line-height: 1.75;
	}

	.hero-actions {
		display: flex;
		align-items: center;
		gap: 34px;
	}

	.text-link,
	.inline-link {
		display: inline-flex;
		align-items: center;
		gap: 11px;
		padding-bottom: 5px;
		border-bottom: 1px solid var(--ink);
		color: var(--ink);
		font-size: 13px;
		font-weight: 700;
	}

	.trust-row {
		display: flex;
		align-items: center;
		gap: 16px;
		margin-top: 43px;
	}

	.avatar-stack {
		display: flex;
	}

	.avatar-stack img {
		width: 35px;
		height: 35px;
		margin-left: -9px;
		border: 2px solid #f8f4e9;
		border-radius: 50%;
		object-fit: cover;
	}

	.avatar-stack img:first-child {
		margin-left: 0;
	}

	.trust-row p {
		margin: 0;
		color: #6c7a77;
		font-size: 11px;
		line-height: 1.5;
	}

	.trust-row strong {
		color: var(--ink);
	}

	.hero-visual {
		position: relative;
		height: 100%;
		min-height: 700px;
	}

	.sun-shape {
		position: absolute;
		top: 112px;
		right: 2%;
		width: 84%;
		aspect-ratio: 1;
		border-radius: 50%;
		background: var(--gold);
	}

	.sun-shape::before,
	.sun-shape::after {
		position: absolute;
		border: 1px solid rgba(20, 95, 82, 0.16);
		border-radius: 50%;
		content: '';
	}

	.sun-shape::before {
		inset: -42px;
	}

	.sun-shape::after {
		inset: -85px;
	}

	.photo-frame {
		position: absolute;
		top: 146px;
		right: 5.5%;
		width: 75%;
		height: 542px;
		overflow: hidden;
		border: 9px solid rgba(255,255,255,.78);
		border-radius: 48% 48% 5px 5px;
		box-shadow: var(--shadow);
		transform: rotate(1.8deg);
	}

	.photo-frame img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		object-position: 53% center;
	}

	.route-card {
		position: absolute;
		z-index: 2;
		top: 215px;
		left: 3%;
		display: flex;
		width: 198px;
		align-items: center;
		gap: 12px;
		padding: 13px 16px;
		border: 1px solid rgba(255, 255, 255, 0.7);
		border-radius: 8px;
		background: rgba(255, 255, 255, 0.91);
		box-shadow: 0 17px 45px rgba(20, 59, 52, 0.15);
		backdrop-filter: blur(8px);
	}

	.route-icon {
		display: grid;
		width: 38px;
		height: 38px;
		border-radius: 50%;
		color: var(--forest);
		background: var(--mint);
		place-items: center;
	}

	.route-icon svg {
		width: 20px;
	}

	.route-card span,
	.route-card strong {
		display: block;
	}

	.route-card span {
		color: #788883;
		font-size: 10px;
	}

	.route-card strong {
		margin-top: 3px;
		font-family: 'Manrope', sans-serif;
		font-size: 14px;
	}

	.destination-chip {
		position: absolute;
		z-index: 2;
		right: 1%;
		bottom: 67px;
		padding: 12px 18px;
		border-radius: 100px;
		color: white;
		background: var(--forest);
		font-size: 10px;
		font-weight: 700;
		letter-spacing: 0.6px;
		text-transform: uppercase;
		transform: rotate(-5deg);
	}

	.destination-chip span {
		padding: 0 5px;
		color: var(--gold);
	}

	.scroll-note {
		position: absolute;
		bottom: 0;
		left: 38px;
		display: flex;
		align-items: center;
		gap: 14px;
		color: #71807d;
		font-size: 8px;
		font-weight: 700;
		letter-spacing: 1.7px;
		transform: rotate(-90deg);
		transform-origin: left center;
	}

	.scroll-note span {
		width: 44px;
		height: 1px;
		background: #9daaa6;
	}

	.section-wrap {
		width: min(1160px, calc(100% - 64px));
		margin-inline: auto;
	}

	.mission {
		padding: 115px 0 0;
		color: white;
		background: var(--forest);
	}

	.mission-grid {
		display: grid;
		grid-template-columns: 1.2fr 0.8fr;
		gap: 130px;
		align-items: start;
	}

	h2 {
		margin-bottom: 0;
		color: var(--ink);
		font-size: clamp(42px, 4.4vw, 64px);
		font-weight: 650;
		line-height: 1.09;
		letter-spacing: -3px;
	}

	.mission h2,
	.mentor-copy h2,
	.cta-section h2 {
		color: white;
	}

	.mission h2 em,
	.mentor-copy h2 em,
	.cta-section h2 em {
		color: var(--gold);
	}

	.mission-copy {
		padding-top: 43px;
	}

	.mission-copy p {
		color: #cee2dc;
		font-size: 15px;
		line-height: 1.75;
	}

	.mission-copy .inline-link {
		margin-top: 13px;
		border-color: #9ec4ba;
		color: white;
	}

	.impact-strip {
		display: grid;
		margin-top: 88px;
		border-top: 1px solid rgba(255,255,255,.14);
		grid-template-columns: repeat(4, 1fr);
	}

	.impact-strip div {
		padding: 35px 20px 38px;
		border-right: 1px solid rgba(255,255,255,.14);
		text-align: center;
	}

	.impact-strip div:last-child {
		border-right: 0;
	}

	.impact-strip strong,
	.impact-strip small {
		display: block;
	}

	.impact-strip strong {
		font-family: 'Manrope', sans-serif;
		font-size: 41px;
		letter-spacing: -1.5px;
	}

	.impact-strip strong span {
		color: var(--gold);
	}

	.impact-strip small {
		margin-top: 7px;
		color: #a8cec4;
		font-size: 8px;
		font-weight: 700;
		letter-spacing: 1.6px;
	}

	.programs {
		padding-block: 116px 128px;
	}

	.programs-header {
		display: grid;
		margin-bottom: 57px;
		grid-template-columns: 1fr 410px;
		gap: 80px;
		align-items: end;
	}

	.programs-header > p {
		margin-bottom: 8px;
		color: var(--muted);
		font-size: 14px;
		line-height: 1.75;
	}

	.program-grid {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		gap: 17px;
	}

	.program-card {
		position: relative;
		min-height: 368px;
		padding: 27px 30px;
		overflow: hidden;
		border-radius: 7px;
	}

	.program-card::after {
		position: absolute;
		right: -42px;
		bottom: -68px;
		width: 170px;
		height: 170px;
		border: 1px solid currentColor;
		border-radius: 50%;
		content: '';
		opacity: .12;
	}

	.program-card.sage { background: #e0efe7; }
	.program-card.sand { background: #f5e9cf; }
	.program-card.coral { background: #f7ded3; }

	.card-top {
		display: flex;
		align-items: start;
		justify-content: space-between;
		color: var(--forest);
	}

	.card-top > span {
		font-family: 'Manrope', sans-serif;
		font-size: 11px;
		font-weight: 700;
	}

	.program-icon {
		display: grid;
		width: 68px;
		height: 68px;
		border-radius: 50%;
		background: rgba(255,255,255,.68);
		place-items: center;
	}

	.program-icon svg { width: 38px; }

	.program-card h3 {
		margin: 42px 0 13px;
		font-size: 24px;
		letter-spacing: -1px;
	}

	.program-card p {
		max-width: 290px;
		color: #5b6f6a;
		font-size: 13px;
		line-height: 1.72;
	}

	.program-card a {
		position: absolute;
		bottom: 31px;
		display: flex;
		gap: 8px;
		border-bottom: 1px solid;
		font-size: 12px;
		font-weight: 700;
	}

	.mentor-band {
		display: grid;
		min-height: 640px;
		grid-template-columns: 1fr 1fr;
		background: var(--forest-dark);
	}

	.mentor-image {
		position: relative;
		overflow: hidden;
	}

	.mentor-image::after {
		position: absolute;
		inset: 0;
		background: linear-gradient(90deg, transparent 75%, var(--forest-dark));
		content: '';
	}

	.mentor-image img {
		width: 100%;
		height: 100%;
		object-fit: cover;
	}

	.availability {
		position: absolute;
		z-index: 2;
		right: 36px;
		bottom: 42px;
		padding: 13px 18px;
		border-radius: 4px;
		color: #183e37;
		background: white;
		font-size: 10px;
		font-weight: 700;
	}

	.availability span {
		display: inline-block;
		width: 7px;
		height: 7px;
		margin-right: 7px;
		border-radius: 50%;
		background: #45ad72;
		box-shadow: 0 0 0 4px rgba(69,173,114,.15);
	}

	.mentor-copy {
		display: flex;
		max-width: 650px;
		padding: 95px 90px;
		flex-direction: column;
		justify-content: center;
	}

	.mentor-copy h2 {
		margin-bottom: 25px;
	}

	.mentor-copy > p {
		color: #bfd7d1;
		font-size: 14px;
		line-height: 1.8;
	}

	.mentor-points {
		display: flex;
		flex-wrap: wrap;
		gap: 22px;
		margin: 14px 0 34px;
		color: white;
		font-size: 11px;
	}

	.mentor-points span::first-letter {
		color: var(--gold);
	}

	.mentor-copy .button {
		align-self: flex-start;
	}

	.stories {
		display: grid;
		padding-block: 120px;
		grid-template-columns: 0.85fr 1.15fr;
		gap: 90px;
		align-items: center;
	}

	.story-controls {
		display: flex;
		gap: 10px;
		margin-top: 44px;
	}

	.story-controls button {
		width: 45px;
		height: 45px;
		border: 1px solid var(--line);
		border-radius: 50%;
		color: var(--forest);
		background: transparent;
		font-size: 18px;
		transition: background .2s ease, color .2s ease;
	}

	.story-controls button:hover {
		color: white;
		background: var(--forest);
	}

	.story-card {
		position: relative;
		min-height: 390px;
		padding: 63px 67px 38px;
		border-radius: 7px;
		background: var(--cream);
	}

	.quote-mark {
		position: absolute;
		top: -37px;
		right: 44px;
		color: var(--gold);
		font-family: Georgia, serif;
		font-size: 130px;
		line-height: 1;
	}

	blockquote {
		margin: 0 0 42px;
		color: var(--ink);
		font-family: Georgia, serif;
		font-size: 25px;
		font-style: italic;
		line-height: 1.55;
	}

	.student {
		display: flex;
		align-items: center;
		gap: 14px;
	}

	.student img {
		width: 51px;
		height: 51px;
		border-radius: 50%;
		object-fit: cover;
	}

	.student strong,
	.student span {
		display: block;
	}

	.student strong { font-size: 12px; }
	.student span { margin-top: 4px; color: var(--muted); font-size: 10px; }

	.story-progress {
		position: absolute;
		right: 37px;
		bottom: 48px;
		display: flex;
		gap: 6px;
	}

	.story-progress button {
		width: 17px;
		height: 3px;
		padding: 0;
		background: #cad1ca;
	}

	.story-progress button.active {
		width: 35px;
		background: var(--forest);
	}

	.resources {
		padding: 115px 0 125px;
		background: #edf4f0;
	}

	.resource-heading {
		display: flex;
		margin-bottom: 55px;
		align-items: end;
		justify-content: space-between;
	}

	.resource-grid {
		display: grid;
		grid-template-columns: 2.1fr 1fr 1fr;
		gap: 17px;
	}

	.feature-resource {
		display: grid;
		min-height: 370px;
		overflow: hidden;
		border-radius: 7px;
		background: white;
		grid-template-columns: 43% 57%;
	}

	.feature-art {
		position: relative;
		display: grid;
		overflow: hidden;
		background: var(--gold);
		place-items: center;
	}

	.feature-art::before,
	.feature-art::after {
		position: absolute;
		border: 1px solid rgba(20,59,52,.21);
		border-radius: 50%;
		content: '';
	}

	.feature-art::before { width: 330px; height: 330px; }
	.feature-art::after { width: 240px; height: 240px; }

	.art-stamp {
		position: absolute;
		z-index: 2;
		top: 25px;
		right: 22px;
		display: grid;
		width: 48px;
		height: 48px;
		border-radius: 50%;
		color: white;
		background: var(--forest);
		font-size: 7px;
		font-weight: 700;
		line-height: 1.4;
		text-align: center;
		place-items: center;
		transform: rotate(8deg);
	}

	.book {
		position: relative;
		z-index: 1;
		display: flex;
		width: 166px;
		height: 225px;
		padding: 24px 20px;
		border-left: 6px solid #dfece6;
		color: white;
		background: var(--forest);
		box-shadow: 16px 16px 28px rgba(20,59,52,.2);
		flex-direction: column;
		transform: rotate(-7deg);
	}

	.book small { font-size: 6px; letter-spacing: 1px; }
	.book strong { margin-top: 37px; font-family: Georgia, serif; font-size: 25px; font-style: italic; font-weight: 400; line-height: 1.03; }
	.book span { margin-top: auto; color: var(--gold); font-size: 6px; font-weight: 700; letter-spacing: 1px; }

	.resource-content {
		display: flex;
		padding: 54px 40px 45px;
		flex-direction: column;
	}

	.tag {
		color: var(--forest);
		font-size: 8px;
		font-weight: 800;
		letter-spacing: 1.5px;
	}

	.resource-content h3,
	.mini-resource h3 {
		margin: 27px 0 14px;
		font-size: 21px;
		line-height: 1.25;
		letter-spacing: -.6px;
	}

	.resource-content p {
		color: var(--muted);
		font-size: 12px;
		line-height: 1.75;
	}

	.resource-content a,
	.mini-resource a {
		display: flex;
		margin-top: auto;
		align-items: center;
		justify-content: space-between;
		padding-top: 16px;
		border-top: 1px solid var(--line);
		color: var(--forest);
		font-size: 11px;
		font-weight: 700;
	}

	.mini-resource {
		display: flex;
		min-height: 370px;
		padding: 30px 27px;
		border-radius: 7px;
		background: #f7e6c7;
		flex-direction: column;
	}

	.mini-resource.green { background: #cfe6da; }

	.mini-icon {
		display: grid;
		width: 57px;
		height: 57px;
		margin-bottom: 34px;
		border-radius: 50%;
		color: var(--forest);
		background: rgba(255,255,255,.62);
		font-family: Georgia, serif;
		font-size: 29px;
		place-items: center;
	}

	.mini-resource h3 {
		margin-top: 20px;
	}

	.cta-section {
		position: relative;
		display: grid;
		min-height: 530px;
		overflow: hidden;
		color: white;
		background: var(--forest);
		text-align: center;
		place-items: center;
	}

	.cta-orbit {
		position: absolute;
		border: 1px solid rgba(255,255,255,.1);
		border-radius: 50%;
	}

	.cta-orbit.one { width: 670px; height: 670px; }
	.cta-orbit.two { width: 950px; height: 950px; }

	.cta-content {
		position: relative;
		z-index: 1;
	}

	.eyebrow.centered { justify-content: center; color: #c7ddd7; }
	.eyebrow.centered span:last-child { display: block; }

	.cta-section h2 {
		font-size: clamp(45px, 5vw, 68px);
	}

	.cta-section p:not(.eyebrow) {
		max-width: 460px;
		margin: 25px auto 32px;
		color: #c5dcd6;
		font-size: 14px;
		line-height: 1.7;
	}

	.cta-actions {
		display: flex;
		align-items: center;
		justify-content: center;
		gap: 32px;
	}

	.cta-actions > a:last-child {
		padding-bottom: 5px;
		border-bottom: 1px solid rgba(255,255,255,.5);
		font-size: 12px;
		font-weight: 700;
	}

	footer {
		color: #afc8c1;
		background: #0d352e;
	}

	.footer-main {
		display: grid;
		padding-block: 70px;
		grid-template-columns: 1.1fr 1.3fr .9fr;
		gap: 80px;
	}

	.brand.inverse { color: white; }
	.brand.inverse .brand-mark { color: var(--gold); }

	.footer-brand p {
		margin: 23px 0;
		font-family: Georgia, serif;
		font-size: 16px;
		font-style: italic;
		line-height: 1.55;
	}

	.socials {
		display: flex;
		gap: 8px;
	}

	.socials a {
		display: grid;
		width: 30px;
		height: 30px;
		border: 1px solid rgba(255,255,255,.2);
		border-radius: 50%;
		color: white;
		font-size: 9px;
		font-weight: 700;
		place-items: center;
	}

	.footer-links {
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 45px;
	}

	.footer-links div {
		display: flex;
		flex-direction: column;
		gap: 13px;
	}

	.footer-links strong,
	.newsletter > strong {
		margin-bottom: 7px;
		color: var(--gold);
		font-size: 8px;
		letter-spacing: 1.4px;
	}

	.footer-links a {
		color: #d6e3df;
		font-size: 12px;
	}

	.newsletter p {
		color: #b7ccc6;
		font-size: 11px;
		line-height: 1.6;
	}

	.newsletter form {
		display: flex;
		margin-top: 20px;
		border-bottom: 1px solid rgba(255,255,255,.35);
	}

	.newsletter input {
		width: 100%;
		padding: 12px 0;
		border: 0;
		outline: 0;
		color: white;
		background: transparent;
		font-size: 11px;
	}

	.newsletter input::placeholder { color: #8aaaa2; }
	.newsletter button { color: var(--gold); background: transparent; }
	.thanks { margin-top: 24px; color: var(--gold); font-size: 12px; }

	.footer-bottom {
		display: flex;
		padding-block: 24px;
		border-top: 1px solid rgba(255,255,255,.1);
		justify-content: space-between;
		font-size: 7px;
		font-weight: 700;
		letter-spacing: 1px;
	}

	.footer-bottom div { display: flex; gap: 26px; }

	.sr-only {
		position: absolute;
		width: 1px;
		height: 1px;
		padding: 0;
		overflow: hidden;
		clip: rect(0, 0, 0, 0);
		white-space: nowrap;
		border: 0;
	}

	@media (max-width: 1050px) {
		.site-header,
		.hero-grid { width: min(100% - 40px, 920px); }
		.site-header nav { gap: 22px; margin-left: 20px; }
		.hero-grid { grid-template-columns: 50% 50%; }
		h1 { font-size: clamp(56px, 7.5vw, 76px); }
		.photo-frame { right: 0; width: 88%; }
		.sun-shape { right: -7%; width: 100%; }
		.section-wrap { width: min(100% - 48px, 920px); }
		.mentor-copy { padding: 70px 50px; }
		.resource-grid { grid-template-columns: 1.6fr 1fr; }
		.mini-resource.green { grid-column: 2; }
		.feature-resource { grid-row: span 2; }
		.footer-main { gap: 40px; }
	}

	@media (max-width: 780px) {
		.site-header {
			position: absolute;
			height: 78px;
		}

		.desktop-cta { display: none; }
		.menu-button { display: block; z-index: 3; }

		nav {
			position: fixed;
			inset: 0;
			display: flex;
			margin: 0;
			padding: 120px 32px;
			visibility: hidden;
			background: #f8f4e9;
			flex-direction: column;
			gap: 28px;
			opacity: 0;
			transition: opacity .2s ease, visibility .2s ease;
		}

		nav.open { visibility: visible; opacity: 1; }
		nav a { font-family: 'Manrope', sans-serif; font-size: 27px; }

		.menu-button.active span:first-child { transform: translateY(3.5px) rotate(45deg); }
		.menu-button.active span:last-child { transform: translateY(-3.5px) rotate(-45deg); }

		.hero { min-height: auto; background: linear-gradient(180deg, #f8f4e9 0 58%, #e3f0eb 58%); }
		.hero-grid { display: block; width: calc(100% - 40px); padding-top: 120px; }
		.hero-copy { padding-top: 30px; }
		h1 { font-size: clamp(53px, 16vw, 76px); letter-spacing: -4px; }
		.hero-lead { font-size: 15px; }
		.hero-visual { min-height: 570px; margin-top: 30px; }
		.photo-frame { top: 55px; right: 5%; width: 84%; height: 450px; }
		.sun-shape { top: 20px; right: 0; width: 92%; }
		.route-card { top: 105px; left: 0; }
		.destination-chip { bottom: 35px; }
		.scroll-note { display: none; }

		.section-wrap { width: calc(100% - 40px); }
		.mission { padding-top: 80px; }
		.mission-grid,
		.programs-header,
		.stories { grid-template-columns: 1fr; gap: 40px; }
		.mission-copy { padding-top: 0; }
		.impact-strip { grid-template-columns: 1fr 1fr; margin-top: 70px; }
		.impact-strip div:nth-child(2) { border-right: 0; }
		.impact-strip div:nth-child(-n+2) { border-bottom: 1px solid rgba(255,255,255,.14); }

		h2 { font-size: clamp(39px, 12vw, 58px); letter-spacing: -2.5px; }
		.programs { padding-block: 80px; }
		.programs-header { margin-bottom: 36px; }
		.program-grid { grid-template-columns: 1fr; }
		.program-card { min-height: 330px; }

		.mentor-band { grid-template-columns: 1fr; }
		.mentor-image { min-height: 430px; }
		.mentor-image::after { background: linear-gradient(180deg, transparent 80%, var(--forest-dark)); }
		.mentor-copy { padding: 70px 30px 80px; }

		.stories { padding-block: 80px; }
		.story-controls { margin-top: 25px; }
		.story-card { min-height: 420px; padding: 55px 35px 35px; }
		blockquote { font-size: 22px; }

		.resources { padding-block: 80px; }
		.resource-heading { align-items: start; flex-direction: column; gap: 30px; }
		.resource-grid { grid-template-columns: 1fr; }
		.feature-resource { grid-row: auto; grid-template-columns: 1fr; }
		.feature-art { min-height: 340px; }
		.mini-resource,
		.mini-resource.green { min-height: 300px; grid-column: auto; }

		.cta-section { min-height: 570px; padding-inline: 20px; }
		.cta-actions { flex-direction: column; }

		.footer-main { grid-template-columns: 1fr; gap: 50px; }
		.footer-bottom { flex-direction: column; gap: 15px; line-height: 1.6; }
	}

	@media (max-width: 480px) {
		.hero-actions { align-items: flex-start; flex-direction: column; gap: 22px; }
		.hero-visual { min-height: 485px; }
		.photo-frame { height: 385px; }
		.route-card { top: 80px; width: 175px; }
		.destination-chip { right: 0; bottom: 20px; }
		.mentor-image { min-height: 350px; }
		.availability { right: 16px; bottom: 25px; }
		.mentor-points { flex-direction: column; gap: 12px; }
		.story-card { min-height: 460px; }
		.story-progress { right: 28px; bottom: 30px; }
	}

	@media (prefers-reduced-motion: reduce) {
		:global(*) {
			scroll-behavior: auto !important;
			transition-duration: 0.01ms !important;
		}
	}
</style>
