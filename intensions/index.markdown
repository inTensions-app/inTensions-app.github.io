---
 # This page uses a custom layout to create a simple, full-screen landing page.
layout: landing
body_class: intensions
privacy_url: /intensions/privacy/
permalink: /intensions/
---

<div class="landing-container">
  <div class="landing-content">
    <h1>inTensions</h1>
    <div class="todo-list-container">
      <a href="{{ site.intensions_google_play_url }}" class="todo-item habit todo-item--cta">
        <div class="todo-item-title">Get it on Google Play</div>
      </a>
      <a href="{{ site.intensions_google_play_url }}" class="todo-item habit">
        <div class="todo-item-title">Do what matters</div>
        <div class="todo-item-subtitle">Last done: Just now<br>(Averaging every day)</div>
      </a>
      <a href="{{ site.intensions_google_play_url }}" class="todo-item">
          <div class="todo-item-title">When your todos are longer than today</div>
          <div class="todo-item-subtitle">Added today</div>
      </a>
      <a href="{{ site.intensions_google_play_url }}" class="todo-item">
        <div class="todo-item-title">Take the paralysis out of analysis</div>
        <div class="todo-item-subtitle overdue">a long time overdue</div>
      </a>
      <a href="{{ site.intensions_google_play_url }}" class="todo-item habit">
        <div class="todo-item-title">No ads, no AI, no nonsense</div>
        <div class="todo-item-subtitle">Last done: Earlier today<br>(Averaging every day)</div>
      </a>
    </div>
    <!-- Snoozed Items Section -->
    <div class="snoozed-list-header">
      <h3>Snoozed</h3>
      <hr>
    </div>
    <div class="todo-list-container">
      <a href="{{ site.intensions_google_play_url }}" class="todo-item snoozed">
        <div class="todo-item-title">Worry about tomorrow</div>
        <div class="todo-item-subtitle">Snoozed until tomorrow</div>
      </a>
    </div>
  </div>
</div>
