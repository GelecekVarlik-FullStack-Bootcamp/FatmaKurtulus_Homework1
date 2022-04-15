USE [master]
GO
/****** Object:  Database [SalesandInventoryManSys]    Script Date: 15.04.2022 09:00:21 ******/
CREATE DATABASE [SalesandInventoryManSys]
 CONTAINMENT = NONE
 ON  PRIMARY 
( NAME = N'SalesandInventoryManSys', FILENAME = N'C:\Program Files\Microsoft SQL Server\MSSQL14.SQLEXPRESS2017\MSSQL\DATA\SalesandInventoryManSys.mdf' , SIZE = 8192KB , MAXSIZE = UNLIMITED, FILEGROWTH = 65536KB )
 LOG ON 
( NAME = N'SalesandInventoryManSys_log', FILENAME = N'C:\Program Files\Microsoft SQL Server\MSSQL14.SQLEXPRESS2017\MSSQL\DATA\SalesandInventoryManSys_log.ldf' , SIZE = 8192KB , MAXSIZE = 2048GB , FILEGROWTH = 65536KB )
GO
ALTER DATABASE [SalesandInventoryManSys] SET COMPATIBILITY_LEVEL = 140
GO
IF (1 = FULLTEXTSERVICEPROPERTY('IsFullTextInstalled'))
begin
EXEC [SalesandInventoryManSys].[dbo].[sp_fulltext_database] @action = 'enable'
end
GO
ALTER DATABASE [SalesandInventoryManSys] SET ANSI_NULL_DEFAULT OFF 
GO
ALTER DATABASE [SalesandInventoryManSys] SET ANSI_NULLS OFF 
GO
ALTER DATABASE [SalesandInventoryManSys] SET ANSI_PADDING OFF 
GO
ALTER DATABASE [SalesandInventoryManSys] SET ANSI_WARNINGS OFF 
GO
ALTER DATABASE [SalesandInventoryManSys] SET ARITHABORT OFF 
GO
ALTER DATABASE [SalesandInventoryManSys] SET AUTO_CLOSE OFF 
GO
ALTER DATABASE [SalesandInventoryManSys] SET AUTO_SHRINK OFF 
GO
ALTER DATABASE [SalesandInventoryManSys] SET AUTO_UPDATE_STATISTICS ON 
GO
ALTER DATABASE [SalesandInventoryManSys] SET CURSOR_CLOSE_ON_COMMIT OFF 
GO
ALTER DATABASE [SalesandInventoryManSys] SET CURSOR_DEFAULT  GLOBAL 
GO
ALTER DATABASE [SalesandInventoryManSys] SET CONCAT_NULL_YIELDS_NULL OFF 
GO
ALTER DATABASE [SalesandInventoryManSys] SET NUMERIC_ROUNDABORT OFF 
GO
ALTER DATABASE [SalesandInventoryManSys] SET QUOTED_IDENTIFIER OFF 
GO
ALTER DATABASE [SalesandInventoryManSys] SET RECURSIVE_TRIGGERS OFF 
GO
ALTER DATABASE [SalesandInventoryManSys] SET  DISABLE_BROKER 
GO
ALTER DATABASE [SalesandInventoryManSys] SET AUTO_UPDATE_STATISTICS_ASYNC OFF 
GO
ALTER DATABASE [SalesandInventoryManSys] SET DATE_CORRELATION_OPTIMIZATION OFF 
GO
ALTER DATABASE [SalesandInventoryManSys] SET TRUSTWORTHY OFF 
GO
ALTER DATABASE [SalesandInventoryManSys] SET ALLOW_SNAPSHOT_ISOLATION OFF 
GO
ALTER DATABASE [SalesandInventoryManSys] SET PARAMETERIZATION SIMPLE 
GO
ALTER DATABASE [SalesandInventoryManSys] SET READ_COMMITTED_SNAPSHOT OFF 
GO
ALTER DATABASE [SalesandInventoryManSys] SET HONOR_BROKER_PRIORITY OFF 
GO
ALTER DATABASE [SalesandInventoryManSys] SET RECOVERY SIMPLE 
GO
ALTER DATABASE [SalesandInventoryManSys] SET  MULTI_USER 
GO
ALTER DATABASE [SalesandInventoryManSys] SET PAGE_VERIFY CHECKSUM  
GO
ALTER DATABASE [SalesandInventoryManSys] SET DB_CHAINING OFF 
GO
ALTER DATABASE [SalesandInventoryManSys] SET FILESTREAM( NON_TRANSACTED_ACCESS = OFF ) 
GO
ALTER DATABASE [SalesandInventoryManSys] SET TARGET_RECOVERY_TIME = 60 SECONDS 
GO
ALTER DATABASE [SalesandInventoryManSys] SET DELAYED_DURABILITY = DISABLED 
GO
ALTER DATABASE [SalesandInventoryManSys] SET QUERY_STORE = OFF
GO
USE [SalesandInventoryManSys]
GO
/****** Object:  Table [dbo].[Customer]    Script Date: 15.04.2022 09:00:21 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Customer](
	[customer_id] [int] IDENTITY(1,1) NOT NULL,
	[customer_name] [nvarchar](20) NOT NULL,
	[customer_mobile] [nvarchar](30) NULL,
	[customer_email] [nvarchar](40) NOT NULL,
	[customer_username] [nvarchar](20) NOT NULL,
	[customer_password] [nvarchar](30) NOT NULL,
	[customer_address] [nvarchar](100) NULL,
 CONSTRAINT [PK_Customer] PRIMARY KEY CLUSTERED 
(
	[customer_id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Inventory]    Script Date: 15.04.2022 09:00:21 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Inventory](
	[inventory_id] [int] IDENTITY(1,1) NOT NULL,
	[inventory_item] [nvarchar](20) NOT NULL,
	[inventory_number] [nvarchar](20) NOT NULL,
	[inventory_type] [nvarchar](30) NOT NULL,
	[inventory_description] [nvarchar](max) NULL,
 CONSTRAINT [PK_Inventory] PRIMARY KEY CLUSTERED 
(
	[inventory_id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Payment]    Script Date: 15.04.2022 09:00:21 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Payment](
	[payment_id] [int] IDENTITY(1,1) NOT NULL,
	[payment_customer_id] [int] NOT NULL,
	[payment_date] [date] NOT NULL,
	[payment_amount] [float] NOT NULL,
	[payment_description] [nvarchar](max) NULL,
	[payment_registration_time] [datetime] NOT NULL,
 CONSTRAINT [PK_Payment] PRIMARY KEY CLUSTERED 
(
	[payment_id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Permission]    Script Date: 15.04.2022 09:00:21 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Permission](
	[permission_id] [int] IDENTITY(1,1) NOT NULL,
	[permission_role_id] [int] NOT NULL,
	[permission_title] [nvarchar](20) NOT NULL,
	[permission_module] [nvarchar](60) NULL,
	[permission_description] [nvarchar](max) NULL,
 CONSTRAINT [PK_Permission] PRIMARY KEY CLUSTERED 
(
	[permission_id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Role]    Script Date: 15.04.2022 09:00:21 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Role](
	[role_id] [int] IDENTITY(1,1) NOT NULL,
	[role_name] [nvarchar](20) NOT NULL,
	[role_description] [nvarchar](max) NULL,
 CONSTRAINT [PK_Role] PRIMARY KEY CLUSTERED 
(
	[role_id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Sales]    Script Date: 15.04.2022 09:00:21 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Sales](
	[sales_id] [int] IDENTITY(1,1) NOT NULL,
	[sales_customer_id] [int] NOT NULL,
	[sales_amount] [float] NOT NULL,
	[sales_type] [nvarchar](30) NOT NULL,
	[sales_description] [nvarchar](max) NULL,
 CONSTRAINT [PK_Sales] PRIMARY KEY CLUSTERED 
(
	[sales_id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Supplier]    Script Date: 15.04.2022 09:00:21 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Supplier](
	[supplier_id] [int] IDENTITY(1,1) NOT NULL,
	[supplier_name] [nvarchar](20) NOT NULL,
	[supplier_mobile] [nvarchar](30) NULL,
	[supplier_email] [nvarchar](50) NOT NULL,
	[supplier_username] [nvarchar](20) NOT NULL,
	[supplier_password] [nvarchar](30) NOT NULL,
	[supplier_address] [nvarchar](100) NULL,
 CONSTRAINT [PK_Supplier] PRIMARY KEY CLUSTERED 
(
	[supplier_id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[User]    Script Date: 15.04.2022 09:00:21 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[User](
	[user_id] [int] IDENTITY(1,1) NOT NULL,
	[user_role_id] [int] NOT NULL,
	[user_name] [nvarchar](20) NOT NULL,
	[user_dob] [datetime] NOT NULL,
	[user_email] [nvarchar](40) NOT NULL,
	[user_address] [nvarchar](60) NULL,
 CONSTRAINT [PK_User] PRIMARY KEY CLUSTERED 
(
	[user_id] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]
GO
ALTER TABLE [dbo].[Payment] ADD  CONSTRAINT [DF_Payment_payment_amount]  DEFAULT ((0)) FOR [payment_amount]
GO
ALTER TABLE [dbo].[Payment] ADD  CONSTRAINT [DF_Payment_payment_registration_time]  DEFAULT (getdate()) FOR [payment_registration_time]
GO
ALTER TABLE [dbo].[Sales] ADD  CONSTRAINT [DF_Sales_sales_amount]  DEFAULT ((0)) FOR [sales_amount]
GO
ALTER TABLE [dbo].[User] ADD  CONSTRAINT [DF_User_user_dob]  DEFAULT (getdate()) FOR [user_dob]
GO
ALTER TABLE [dbo].[Payment]  WITH CHECK ADD  CONSTRAINT [FK_Payment_Customer] FOREIGN KEY([payment_customer_id])
REFERENCES [dbo].[Customer] ([customer_id])
GO
ALTER TABLE [dbo].[Payment] CHECK CONSTRAINT [FK_Payment_Customer]
GO
ALTER TABLE [dbo].[Permission]  WITH CHECK ADD  CONSTRAINT [FK_Permission_Role] FOREIGN KEY([permission_role_id])
REFERENCES [dbo].[Role] ([role_id])
GO
ALTER TABLE [dbo].[Permission] CHECK CONSTRAINT [FK_Permission_Role]
GO
ALTER TABLE [dbo].[Sales]  WITH CHECK ADD  CONSTRAINT [FK_Sales_Customer] FOREIGN KEY([sales_customer_id])
REFERENCES [dbo].[Customer] ([customer_id])
GO
ALTER TABLE [dbo].[Sales] CHECK CONSTRAINT [FK_Sales_Customer]
GO
ALTER TABLE [dbo].[User]  WITH CHECK ADD  CONSTRAINT [FK_User_Role] FOREIGN KEY([user_role_id])
REFERENCES [dbo].[Role] ([role_id])
GO
ALTER TABLE [dbo].[User] CHECK CONSTRAINT [FK_User_Role]
GO
USE [master]
GO
ALTER DATABASE [SalesandInventoryManSys] SET  READ_WRITE 
GO
