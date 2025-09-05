---
# This page uses a custom layout to create a simple, full-screen landing page.
layout: landing
---

<div class="landing-container">
  <div class="landing-content">
    <h1>inTensions</h1>
    <a href="https://play.google.com/store/apps/details?id=com.yourapp.package" class="button">
      Get it on Google Play
    </a>
        <div class="todo-list-container">   
      <div class="todo-item habit">
        <div class="todo-item-title">Do what matters</div>
        <div class="todo-item-subtitle">Last done: Just now<br>(Averaging every day)</div>
      </div>
      <div class="todo-item">
          <div class="todo-item-title">When your todos are longer than today</div>
          <div class="todo-item-subtitle">Added today</div>
      </div>
      <div class="todo-item">
        <div class="todo-item-title">Take the paralysis out of analysis</div>
        <div class="todo-item-subtitle overdue">a long time overdue</div>
      </div>
      <div class="todo-item habit">
        <div class="todo-item-title">No ads, no AI, no nonsense</div>
        <div class="todo-item-subtitle">Last done: Earlier today<br>(Averaging every day)</div>
      </div>
    </div>
    <!-- Snoozed Items Section -->
    <div class="snoozed-list-header">
      <h3>Snoozed</h3>
      <hr>
    </div>
    <div class="todo-list-container">
      <div class="todo-item snoozed">
        <div class="todo-item-title">worry about tomorrow</div>
        <div class="todo-item-subtitle">Snoozed until tomorrow</div>
      </div>
    </div>

  </div>
  <div class="contact-info">
    <a href="mailto:{{ site.email }}">{{ site.email }}</a>
  </div>
</div>