# Migration v1

```sql
-- Current sql file was generated after introspecting the database
-- If you want to run this migration please uncomment this code before executing migrations

CREATE TYPE "public"."concept" AS ENUM('work', 'training', 'break', 'lunch', 'medical', 'other');--> statement-breakpoint
CREATE TYPE "public"."device" AS ENUM('mobile', 'tablet', 'desktop');--> statement-breakpoint
CREATE TYPE "public"."time_entry_type" AS ENUM('start', 'end');--> statement-breakpoint
CREATE TYPE "public"."timezone" AS ENUM('UTC', 'CET', 'Atlantic/Canary');--> statement-breakpoint
CREATE TYPE "public"."user_role" AS ENUM('admin', 'manager', 'employee');--> statement-breakpoint
CREATE TYPE "public"."user_status" AS ENUM('pending', 'active', 'blocked');--> statement-breakpoint
CREATE TABLE "locations" (
"id" text PRIMARY KEY NOT NULL,
"name" text NOT NULL,
"slug" text NOT NULL,
"latitude" text,
"longitude" text,
"street_address" text,
"street_number" text,
"floor" text,
"door" text,
"postal_code" text,
"city" text,
"province" text,
"country" text,
"phone" text,
"email" text,
"opening_time" time,
"closing_time" time,
"timezone" timezone DEFAULT 'CET' NOT NULL,
"organization_id" text NOT NULL,
"created_at" timestamp DEFAULT now() NOT NULL,
"updated_at" timestamp DEFAULT now() NOT NULL,
CONSTRAINT "locations_slug_unique" UNIQUE("slug")
);
--> statement-breakpoint
CREATE TABLE "users" (
"id" text PRIMARY KEY NOT NULL,
"clerk_user_id" text NOT NULL,
"email" varchar(256) NOT NULL,
"first_name" varchar(256),
"last_name" varchar(256),
"role" "user_role" DEFAULT 'employee' NOT NULL,
"status" "user_status" DEFAULT 'pending' NOT NULL,
"image_url" text,
"job_title" text,
"linkedin_url" text,
"organization_id" text NOT NULL,
"department_id" text,
"created_at" timestamp DEFAULT now() NOT NULL,
"updated_at" timestamp DEFAULT now() NOT NULL,
"last_login_at" timestamp,
"location_id" text,
CONSTRAINT "users_clerk_user_id_unique" UNIQUE("clerk_user_id"),
CONSTRAINT "users_email_unique" UNIQUE("email")
);
--> statement-breakpoint
CREATE TABLE "absence_requests" (
"id" text PRIMARY KEY NOT NULL,
"user_id" text NOT NULL,
"type" text NOT NULL,
"start_date" timestamp NOT NULL,
"end_date" timestamp NOT NULL,
"notes" text,
"status" text DEFAULT 'pending' NOT NULL,
"created_at" timestamp DEFAULT CURRENT_TIMESTAMP NOT NULL
);
--> statement-breakpoint
CREATE TABLE "calendars" (
"id" text PRIMARY KEY NOT NULL,
"organization_id" text NOT NULL,
"name" text NOT NULL,
"created_at" timestamp DEFAULT now() NOT NULL
);
--> statement-breakpoint
CREATE TABLE "organizations" (
"id" text PRIMARY KEY NOT NULL,
"name" text NOT NULL,
"slug" text NOT NULL,
"tagline" text,
"description" text,
"logo" text,
"address" text,
"phone" text,
"email" text,
"website" text,
"created_at" timestamp DEFAULT now() NOT NULL,
"updated_at" timestamp DEFAULT now() NOT NULL,
CONSTRAINT "organizations_slug_unique" UNIQUE("slug")
);
--> statement-breakpoint
CREATE TABLE "departments" (
"id" text PRIMARY KEY NOT NULL,
"name" text NOT NULL,
"description" text,
"organization_id" text NOT NULL,
"created_at" timestamp DEFAULT now() NOT NULL,
"updated_at" timestamp DEFAULT now() NOT NULL
);
--> statement-breakpoint
CREATE TABLE "time_entry_cancellations" (
"id" text PRIMARY KEY NOT NULL,
"time_entry_id" text NOT NULL,
"cancelled_by" text NOT NULL,
"cancellation_reason" text NOT NULL,
"cancelled_at" timestamp DEFAULT now() NOT NULL
);
--> statement-breakpoint
CREATE TABLE "time_entries" (
"id" text PRIMARY KEY NOT NULL,
"user_id" text NOT NULL,
"type" time_entry_type NOT NULL,
"concept" "concept" NOT NULL,
"timestamp" timestamp DEFAULT now() NOT NULL,
"notes" text,
"location" text,
"device" "device" NOT NULL,
"application" text DEFAULT 'Fichajes' NOT NULL,
"is_incidence" boolean DEFAULT false,
"created_at" timestamp DEFAULT now() NOT NULL
);
--> statement-breakpoint
CREATE TABLE "calendar_events" (
"id" text PRIMARY KEY NOT NULL,
"calendar_id" text NOT NULL,
"type" text NOT NULL,
"date" timestamp NOT NULL,
"name" text NOT NULL,
"created_at" timestamp DEFAULT now() NOT NULL
);
--> statement-breakpoint
CREATE TABLE "absences" (
"id" text PRIMARY KEY NOT NULL,
"user_id" text NOT NULL,
"type" text NOT NULL,
"start_date" timestamp NOT NULL,
"end_date" timestamp NOT NULL,
"status" text NOT NULL,
"notes" text,
"created_at" timestamp DEFAULT now() NOT NULL
);
--> statement-breakpoint
ALTER TABLE "locations" ADD CONSTRAINT "locations_organization_id_organizations_id_fk" FOREIGN KEY ("organization_id") REFERENCES "public"."organizations"("id") ON DELETE no action ON UPDATE no action;--> statement-breakpoint
ALTER TABLE "users" ADD CONSTRAINT "users_organization_id_organizations_id_fk" FOREIGN KEY ("organization_id") REFERENCES "public"."organizations"("id") ON DELETE no action ON UPDATE no action;--> statement-breakpoint
ALTER TABLE "users" ADD CONSTRAINT "users_department_id_departments_id_fk" FOREIGN KEY ("department_id") REFERENCES "public"."departments"("id") ON DELETE no action ON UPDATE no action;--> statement-breakpoint
ALTER TABLE "users" ADD CONSTRAINT "users_location_id_locations_id_fk" FOREIGN KEY ("location_id") REFERENCES "public"."locations"("id") ON DELETE no action ON UPDATE no action;--> statement-breakpoint
ALTER TABLE "calendars" ADD CONSTRAINT "calendars_organization_id_organizations_id_fk" FOREIGN KEY ("organization_id") REFERENCES "public"."organizations"("id") ON DELETE no action ON UPDATE no action;--> statement-breakpoint
ALTER TABLE "departments" ADD CONSTRAINT "departments_organization_id_organizations_id_fk" FOREIGN KEY ("organization_id") REFERENCES "public"."organizations"("id") ON DELETE no action ON UPDATE no action;--> statement-breakpoint
ALTER TABLE "time_entry_cancellations" ADD CONSTRAINT "time_entry_cancellations_time_entry_id_time_entries_id_fk" FOREIGN KEY ("time_entry_id") REFERENCES "public"."time_entries"("id") ON DELETE no action ON UPDATE no action;--> statement-breakpoint
ALTER TABLE "time_entry_cancellations" ADD CONSTRAINT "time_entry_cancellations_cancelled_by_users_id_fk" FOREIGN KEY ("cancelled_by") REFERENCES "public"."users"("id") ON DELETE no action ON UPDATE no action;--> statement-breakpoint
ALTER TABLE "time_entries" ADD CONSTRAINT "time_entries_user_id_users_id_fk" FOREIGN KEY ("user_id") REFERENCES "public"."users"("id") ON DELETE no action ON UPDATE no action;--> statement-breakpoint
ALTER TABLE "calendar_events" ADD CONSTRAINT "calendar_events_calendar_id_calendars_id_fk" FOREIGN KEY ("calendar_id") REFERENCES "public"."calendars"("id") ON DELETE no action ON UPDATE no action;--> statement-breakpoint
ALTER TABLE "absences" ADD CONSTRAINT "absences_user_id_users_id_fk" FOREIGN KEY ("user_id") REFERENCES "public"."users"("id") ON DELETE no action ON UPDATE no action;
```
